<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>Live Smile Detection</title>

    <!-- MediaPipe Libraries -->
    <script src="https://cdn.jsdelivr.net/npm/@mediapipe/camera_utils/camera_utils.js"
        crossorigin="anonymous"></script>

    <script src="https://cdn.jsdelivr.net/npm/@mediapipe/face_mesh/face_mesh.js"
        crossorigin="anonymous"></script>

    <style>
        body {
            font-family: Arial, sans-serif;
            background: #eef2f7;
            text-align: center;
            margin: 0;
            padding: 20px;
        }

        h1 {
            color: #173b70;
        }

        .container {
            max-width: 800px;
            margin: auto;
            background: white;
            padding: 20px;
            border-radius: 15px;
            box-shadow: 0 4px 12px #bbb;
        }

        video {
            display: none;
        }

        canvas {
            width: 100%;
            max-width: 640px;
            border: 3px solid #173b70;
            border-radius: 10px;
            background: #222;
        }

        #status {
            font-size: 24px;
            font-weight: bold;
            color: #173b70;
            margin: 15px;
        }

        #details {
            font-size: 16px;
            color: #444;
        }

        button {
            padding: 12px 25px;
            margin: 8px;
            border: none;
            border-radius: 8px;
            font-size: 16px;
            cursor: pointer;
        }

        #startButton {
            background: #16834a;
            color: white;
        }

        #stopButton {
            background: #c93636;
            color: white;
        }

        button:hover {
            opacity: 0.8;
        }

        .note {
            color: #666;
            font-size: 14px;
        }
    </style>
</head>

<body>

    <div class="container">

        <h1>😊 Live Smile Detection</h1>

        <p>
            Turn on your webcam and smile at the camera.
        </p>

        <video id="inputVideo" autoplay playsinline></video>

        <canvas id="outputCanvas"
            width="640" height="480"></canvas>

        <div id="status">Camera is not started</div>

        <p id="details">
            Click Start Camera to begin detection.
        </p>

        <button id="startButton">
            Start Camera
        </button>

        <button id="stopButton">
            Stop Camera
        </button>

        <p class="note">
            Allow camera permission when your browser asks.
        </p>

    </div>

    <script>
        const video = document.getElementById("inputVideo");

        const canvas = document.getElementById("outputCanvas");

        const ctx = canvas.getContext("2d");

        const statusText = document.getElementById("status");

        const details = document.getElementById("details");

        const startButton = document.getElementById("startButton");

        const stopButton = document.getElementById("stopButton");

        let camera = null;

        let faceMesh = null;

        let running = false;

        function showMessage(message, color) {
            statusText.textContent = message;
            statusText.style.color = color;
        }

        function calculateDistance(point1, point2) {
            const dx = point1.x - point2.x;
            const dy = point1.y - point2.y;

            return Math.sqrt(dx * dx + dy * dy);
        }

        function detectSmile(landmarks) {
            // MediaPipe Face Mesh lip landmark points
            const leftCorner = landmarks[61];
            const rightCorner = landmarks[291];

            const upperLip = landmarks[13];
            const lowerLip = landmarks[14];

            const leftCheek = landmarks[234];
            const rightCheek = landmarks[454];

            const mouthWidth = calculateDistance(
                leftCorner, rightCorner
            );

            const mouthHeight = calculateDistance(
                upperLip, lowerLip
            );

            const faceWidth = calculateDistance(
                leftCheek, rightCheek
            );

            if (faceWidth === 0) {
                return false;
            }

            const widthRatio = mouthWidth / faceWidth;
            const heightRatio = mouthHeight / mouthWidth;

            // Approximate smile detection rule.
            // Thresholds may need adjustment for each face.
            return widthRatio > 0.32 &&
                   heightRatio > 0.04 &&
                   heightRatio < 0.30;
        }

        function onResults(results) {
            if (!running) {
                return;
            }

            ctx.clearRect(0, 0, canvas.width, canvas.height);

            ctx.save();

            ctx.drawImage(
                results.image,
                0, 0,
                canvas.width,
                canvas.height
            );

            if (results.multiFaceLandmarks &&
                results.multiFaceLandmarks.length > 0) {

                const landmarks =
                    results.multiFaceLandmarks[0];

                const smiling = detectSmile(landmarks);

                const leftCorner = landmarks[61];
                const rightCorner = landmarks[291];

                // Draw a box around the mouth.
                const x = leftCorner.x * canvas.width;
                const y = leftCorner.y * canvas.height;

                const x2 = rightCorner.x * canvas.width;
                const y2 = rightCorner.y * canvas.height;

                ctx.strokeStyle = smiling ? "#00ff00" : "#ffff00";
                ctx.lineWidth = 3;

                ctx.beginPath();
                ctx.moveTo(x, y);
                ctx.lineTo(x2, y2);
                ctx.stroke();

                if (smiling) {
                    showMessage("😊 Smile Detected!", "#16834a");

                    details.textContent =
                        "A possible smile was detected on your face.";

                    ctx.fillStyle = "#00ff00";
                    ctx.font = "bold 26px Arial";

                    ctx.fillText(
                        "SMILING!",
                        20,
                        40
                    );
                } else {
                    showMessage("😐 No Smile Detected", "#c93636");

                    details.textContent =
                        "Try smiling at the webcam.";
                }

            } else {
                showMessage("No Face Detected", "#c93636");

                details.textContent =
                    "Move your face into the camera view.";
            }

            ctx.restore();
        }

        async function startCamera() {
            if (running) {
                return;
            }

            showMessage("Loading detector...", "#173b70");

            details.textContent =
                "Please wait while the face detector loads.";

            try {
                faceMesh = new FaceMesh({
                    locateFile: (file) =>
                        "https://cdn.jsdelivr.net/npm/@mediapipe/face_mesh/" + file
                });

                faceMesh.setOptions({
                    maxNumFaces: 1,
                    refineLandmarks: true,
                    minDetectionConfidence: 0.5,
                    minTrackingConfidence: 0.5
                });

                faceMesh.onResults(onResults);

                camera = new Camera(video, {
                    onFrame: async () => {
                        if (running) {
                            await faceMesh.send({
                                image: video
                            });
                        }
                    },
                    width: 640,
                    height: 480
                });

                running = true;

                await camera.start();

                showMessage("Camera Started", "#16834a");

                details.textContent =
                    "Look at the webcam and smile!";

            } catch (error) {
                running = false;

                showMessage("Camera Error", "#c93636");

                details.textContent =
                    "Allow camera access and use a supported browser. " +
                    "Check your internet connection and try again.";

                console.error(error);
            }
        }

        function stopCamera() {
            running = false;

            if (camera && camera.video) {
                const stream = camera.video.srcObject;

                if (stream) {
                    stream.getTracks().forEach(
                        track => track.stop()
                    );
                }
            }

            if (video.srcObject) {
                video.srcObject.getTracks().forEach(
                    track => track.stop()
                );

                video.srcObject = null;
            }

            ctx.clearRect(0, 0, canvas.width, canvas.height);

            showMessage("Camera Stopped", "#173b70");

            details.textContent =
                "Click Start Camera to detect smiles again.";
        }

        startButton.addEventListener(
            "click",
            startCamera
        );

        stopButton.addEventListener(
            "click",
            stopCamera
        );

    </script>

</body>
</html>
