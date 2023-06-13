<script>
	// @ts-nocheck

	import * as THREE from 'three';
	import { OBJLoader } from 'three/examples/jsm/loaders/OBJLoader';
	import * as THREEx from '@ar-js-org/ar.js/three.js/build/ar-threex.js';
	import { onMount, onDestroy } from 'svelte';
	import Card, { Content, PrimaryAction } from '@smui/card';
	import IconButton from '@smui/icon-button';
	let clicked = 0;

	let canvas;

	let currentGuideNumber = 0;

	let cube;
	let lewarek;
	let arrows;
	let wrench;
	let wrenchReverse;

	const objects = {};

	const all = [];

	const steps = [
		{
			text: 'Wrzuć bieg',
			isAR: false,
		},
		{
			text: 'Wyjmij koło zapasowe z bagażnika lub kosza',
			isAR: false,
		},
		{
			text: 'Zablokuj drugie koło na tej samej osi',
			isAR: true,
			functionn: () => {
				cube.visible = true;
			},
		},
		{
			text: 'Unieś auto za pomocą lewarka',
			isAR: true,
			functionn: () => {
				lewarek.visible = true;
			},
		},
		{
			text: 'Odkręć śruby fabrycznym kluczem',
			isAR: true,
			functionn: () => {
				wrench.visible = true;
			},
		},
		{
			text: 'Wymień koło',
			isAR: false,
		},
		{
			text: 'Przykręć śruby',
			isAR: true,
			functionn: () => {
				wrenchReverse.visible = true;
			},
		},
		{
			text: 'Po przejechaniu kilku kilometrów, zatrzymaj się i sprawdź, czy dobrze zamontowałeś koło',
			isAR: false,
		},
	];

	const handleChange = () => {
		all.forEach((obj) => (obj.visible = false));
		if (steps[currentGuideNumber].isAR) {
			steps[currentGuideNumber].functionn();
		}
	};

	const handlePlus = () => {
		currentGuideNumber < steps.length - 1 && currentGuideNumber++;
		handleChange();
	};
	const handleMinus = () => {
		currentGuideNumber > 0 && currentGuideNumber--;
		handleChange();
	};

	let width = 393,
		height = 696;

	onDestroy(() => {
		const videoEl = document.getElementById('arjs-video');
		if (videoEl) {
			const stream = videoEl.srcObject;
			if (stream) {
				const tracks = stream.getTracks();

				tracks.forEach(function (track) {
					track.stop();
				});
				videoEl.remove();
			}
		}
	});

	onMount(() => {
		THREEx.ArToolkitContext.baseURL =
			'https://raw.githubusercontent.com/LucaJunge/arjs-vue/main/public/';

		//////////////////////////////////////////////////////////////////////////////////
		//		Init
		//////////////////////////////////////////////////////////////////////////////////

		// init renderer
		var renderer = new THREE.WebGLRenderer({
			antialias: true,
			alpha: true,
		});
		renderer.setClearColor(new THREE.Color('lightgrey'), 0);
		renderer.setSize(640, 480);
		renderer.domElement.style.position = 'absolute';
		renderer.domElement.style.top = '0px';
		renderer.domElement.style.left = '0px';
		document.body.appendChild(renderer.domElement);

		// array of functions for the rendering loop
		var onRenderFcts = [];
		var arToolkitContext, arMarkerControls;

		// init scene and camera
		var scene = new THREE.Scene();

		//////////////////////////////////////////////////////////////////////////////////
		//		Initialize a basic camera
		//////////////////////////////////////////////////////////////////////////////////

		// Create a camera
		var camera = new THREE.Camera();
		scene.add(camera);

		////////////////////////////////////////////////////////////////////////////////
		//          handle arToolkitSource
		////////////////////////////////////////////////////////////////////////////////

		var arToolkitSource = new THREEx.ArToolkitSource({
			// to read from the webcam
			sourceType: 'webcam',

			sourceWidth: window.innerWidth > window.innerHeight ? 640 : 480,
			sourceHeight: window.innerWidth > window.innerHeight ? 480 : 640,

			// // to read from an image
			// sourceType : 'image',
			// sourceUrl : THREEx.ArToolkitContext.baseURL + '../data/images/img.jpg',

			// to read from a video
			// sourceType : 'video',
			// sourceUrl : THREEx.ArToolkitContext.baseURL + '../data/videos/headtracking.mp4',
		});

		arToolkitSource.init(function onReady() {
			arToolkitSource.domElement.addEventListener('canplay', () => {
				console.log(
					'canplay',
					'actual source dimensions',
					arToolkitSource.domElement.videoWidth,
					arToolkitSource.domElement.videoHeight
				);

				initARContext();
			});
			window.arToolkitSource = arToolkitSource;
			setTimeout(() => {
				onResize();
			}, 2000);
		});

		// handle resize
		window.addEventListener('resize', function () {
			onResize();
		});

		window.addEventListener('arjs-nft-loaded', function (ev) {
			console.log(ev);
			console.log('TUUUUUUUUUUU');
		});

		function onResize() {
			// arToolkitSource.onResizeElement();
			// arToolkitSource.copyElementSizeTo(renderer.domElement);
			// if (window.arToolkitContext.arController !== null) {
			// 	arToolkitSource.copyElementSizeTo(
			// 		window.arToolkitContext.arController.canvas
			// 	);
			// }
		}
		////////////////////////////////////////////////////////////////////////////////
		//          initialize arToolkitContext
		////////////////////////////////////////////////////////////////////////////////

		function initARContext() {
			// create atToolkitContext
			arToolkitContext = new THREEx.ArToolkitContext({
				cameraParametersUrl:
					THREEx.ArToolkitContext.baseURL + '/data/camera_para.dat',
				detectionMode: 'mono',
				imageSmoothingEnabled: true,
			});
			// initialize it
			arToolkitContext.init(() => {
				// copy projection matrix to camera
				camera.projectionMatrix.copy(arToolkitContext.getProjectionMatrix());

				arToolkitContext.arController.orientation = getSourceOrientation();
				arToolkitContext.arController.options.orientation =
					getSourceOrientation();

				console.log('arToolkitContext', arToolkitContext);
				window.arToolkitContext = arToolkitContext;
			});

			// MARKER
			arMarkerControls = new THREEx.ArMarkerControls(arToolkitContext, camera, {
				type: 'pattern',
				patternUrl: '/public/models/pattern/pattern-wheel223.patt',
				// patternUrl: THREEx.ArToolkitContext.baseURL + '/data/patt.hiro',
				// patternUrl : THREEx.ArToolkitContext.baseURL + '../data/data/patt.kanji',
				// as we controls the camera, set changeMatrixMode: 'cameraTransformMatrix'
				changeMatrixMode: 'cameraTransformMatrix',
				smooth: true,
				smoothCount: 5,
				smoothTolerance: 0.01,
				smoothThreshold: 2,
			});
			// NEW MARKER
			// arMarkerControls = new THREEx.ArMarkerControls(arToolkitContext, camera, {
			// 	type: 'nft',
			// 	descriptorsUrl:
			// 		'https://github.com/AR-js-org/.github/raw/main/profile/aframe/examples/image-tracking/nft/trex/trex-image/trex',
			// 	// patternUrl : THREEx.ArToolkitContext.baseURL + '../data/data/patt.kanji',
			// 	// as we controls the camera, set changeMatrixMode: 'cameraTransformMatrix'
			// 	changeMatrixMode: 'cameraTransformMatrix',
			// });

			scene.visible = false;

			console.log('ArMarkerControls', arMarkerControls);
			window.arMarkerControls = arMarkerControls;
		}

		function getSourceOrientation() {
			if (!arToolkitSource) {
				return null;
			}

			console.log(
				'actual source dimensions',
				arToolkitSource.domElement.videoWidth,
				arToolkitSource.domElement.videoHeight
			);

			if (
				arToolkitSource.domElement.videoWidth >
				arToolkitSource.domElement.videoHeight
			) {
				console.log('source orientation', 'landscape');
				return 'landscape';
			} else {
				console.log('source orientation', 'portrait');
				return 'landscape';
			}
		}

		// update artoolkit on every frame
		onRenderFcts.push(function () {
			if (!arToolkitContext || !arToolkitSource || !arToolkitSource.ready) {
				return;
			}

			arToolkitContext.update(arToolkitSource.domElement);

			// update scene.visible if the marker is seen
			scene.visible = camera.visible;
		});

		//////////////////////////////////////////////////////////////////////////////////
		//		add an object in the scene
		//////////////////////////////////////////////////////////////////////////////////

		// add a torus knot
		var geometry = new THREE.BoxGeometry(1, 1, 1);
		var material = new THREE.MeshNormalMaterial({
			transparent: true,
			opacity: 0.5,
			side: THREE.DoubleSide,
		});

		// var mesh = new THREE.Mesh(geometry, material);
		// mesh.position.y = geometry.parameters.height / 2;
		// scene.add(mesh);

		// var geometry = new THREE.TorusKnotGeometry(0.3, 0.1, 64, 16);
		// var material = new THREE.MeshNormalMaterial();
		// var mesh = new THREE.Mesh(geometry, material);
		// mesh.position.y = 0.5;
		// scene.add(mesh);

		//===============================================
		//=============================================== Funkcje
		//===============================================

		//=============================================== Definicje
		const loader = new OBJLoader();

		const redMaterial = new THREE.MeshPhongMaterial({ color: 0xff0000 });
		const greenMaterial = new THREE.MeshPhongMaterial({ color: 0x00ff00 });
		const blueMaterial = new THREE.MeshPhongMaterial({ color: 0x0000ff });
		// let wrenchReverse;

		//=============================================== Box
		var mesh = new THREE.Mesh(geometry, blueMaterial);
		mesh.scale.set(0.1, 0.1, 0.1);
		mesh.position.set(0.165, 0, 0.183);

		cube = mesh;
		all.push(cube);
		scene.add(mesh);

		//=============================================== Lewarek
		loader.load('/public/models/lewarek.obj', function (mesh) {
			mesh.scale.set(0.08, 0.08, 0.08);
			mesh.position.set(0.26, 0, 0.12);
			mesh.rotation.set(Math.PI / 2, 0, 0);
			mesh.traverse(function (child) {
				if (child) {
					child.material = redMaterial;
				}
			});
			lewarek = mesh;
			all.push(lewarek);
			scene.add(mesh);
		});

		//=============================================== Strzalki
		// loader.load('/public/models/arrows2.obj', function (mesh) {
		// 	mesh.scale.set(0.02, 0.02, 0.02);
		// 	mesh.rotation.set(Math.PI / 2, 0, 0);
		// 	mesh.traverse(function (child) {
		// 		if (child) {
		// 			child.material = redMaterial;
		// 		}
		// 	});
		// 	arrows = mesh;
		// 	all.push(arrows);
		// 	scene.add(mesh);
		// });

		//======================================== klucz
		loader.load('/public/models/wrench.obj', function (mesh) {
			mesh.scale.set(0.003, 0.003, 0.003);
			mesh.position.set(-0.07, 0, 0.12);
			mesh.rotation.set(Math.PI / 2, 0, 0);
			mesh.traverse(function (child) {
				if (child) {
					child.material = greenMaterial;
				}
			});
			wrench = mesh;
			all.push(wrench);
			scene.add(mesh);
		});

		//======================================== wrenchReverse
		loader.load('/public/models/wrench.obj', function (mesh) {
			mesh.scale.set(0.003, 0.003, 0.003);
			mesh.position.set(-0.07, 0, 0.12);
			mesh.rotation.set(Math.PI / 2, 0, 0);
			mesh.traverse(function (child) {
				if (child) {
					child.material = greenMaterial;
				}
			});
			wrenchReverse = mesh;
			all.push(wrenchReverse);
			scene.add(mesh);
		});

		//========================================

		var light = new THREE.PointLight(0xffffff, 1, 500);
		light.position.set(10, 10, 25);
		scene.add(light);

		onRenderFcts.push(function (delta) {
			// arrows.rotation.z -= Math.PI * delta * 0.5;
			wrench.rotation.z -= Math.PI * delta * 0.5;
			wrenchReverse.rotation.z += Math.PI * delta * 0.5;
		});

		//////////////////////////////////////////////////////////////////////////////////
		//		render the whole thing on the page
		//////////////////////////////////////////////////////////////////////////////////

		// render the scene
		onRenderFcts.push(function () {
			renderer.render(scene, camera);
		});

		// run the rendering loop
		var lastTimeMsec = null;
		requestAnimationFrame(function animate(nowMsec) {
			// keep looping
			requestAnimationFrame(animate);
			// measure time
			lastTimeMsec = lastTimeMsec || nowMsec - 1000 / 60;
			var deltaMsec = Math.min(200, nowMsec - lastTimeMsec);
			lastTimeMsec = nowMsec;
			// call each update function
			onRenderFcts.forEach(function (onRenderFct) {
				onRenderFct(deltaMsec / 1000, nowMsec / 1000);
			});
		});
	});
</script>

<div id="ARScene" bind:this={canvas} class="ar-container" />
<!-- class:notAR={!steps[currentGuideNumber].isAR} -->
<div id="guide" class="guide">
	<Card>
		<PrimaryAction on:click={() => clicked++}>
			<Content class="mdc-typography--body2">
				<h5
					class="mdc-typography--headline6"
					style="margin: 0; font-weight: 400"
				>
					{steps[currentGuideNumber].text}
				</h5>
			</Content>
		</PrimaryAction>
	</Card>
	<div>
		<IconButton
			class="material-icons"
			style="width: 60px; height: 60px"
			on:click={handleMinus}
		>
			arrow_left
		</IconButton>
		<IconButton
			class="material-icons"
			style="width: 60px; height: 60px"
			on:click={handlePlus}
		>
			arrow_right
		</IconButton>
	</div>
</div>

<style>
	.ar-container {
		position: relative;
		width: 100%;
		height: 100%;
	}
	.guide {
		position: absolute;
		bottom: 56px;
		width: 350px;
		/* background-color: blue; */
		height: 200px;
		z-index: 20;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		font-size: 25px;
		padding: 20px;
	}
	.isAR {
		height: 700px;
	}
	.notAR {
		height: 200px;
	}
</style>
