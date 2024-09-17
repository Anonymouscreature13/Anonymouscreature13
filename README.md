<!DOCTYPE html>
<html>
<head>
    <title>Camera, Microphone, aur Location Access</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            padding: 20px;
            text-align: center;
        }
        #video {
            width: 100%;
            max-width: 600px;
            border: 1px solid black;
        }
        button {
            padding: 10px 20px;
            font-size: 16px;
            cursor: pointer;
        }
    </style>
</head>
<body>
    <h1>Camera aur Microphone Access</h1>
    <video id="video" autoplay></video>

    <h1>Location Access</h1>
    <button onclick="getLocation()">Location Pata Karein</button>
    <p id="location"></p>

    <script>
        // Camera aur Microphone access maangna
        navigator.mediaDevices.getUserMedia({ video: true, audio: true })
        .then(function(stream) {
            var video = document.getElementById('video');
            video.srcObject = stream;
        })
        .catch(function(err) {
            console.log("Error: " + err);
        });

        // Location access maangna
        function getLocation() {
            if (navigator.geolocation) {
                navigator.geolocation.getCurrentPosition(showPosition, showError);
            } else {
                document.getElementById("location").innerHTML = "Geolocation is not supported by this browser.";
            }
        }

        function showPosition(position) {
            document.getElementById("location").innerHTML = 
                "Latitude: " + position.coords.latitude + 
                "<br>Longitude: " + position.coords.longitude;
        }

        function showError(error) {
            switch(error.code) {
                case error.PERMISSION_DENIED:
                    document.getElementById("location").innerHTML = "User ne Geolocation ki request ko deny kar diya.";
                    break;
                case error.POSITION_UNAVAILABLE:
                    document.getElementById("location").innerHTML = "Location information available nahi hai.";
                    break;
                case error.TIMEOUT:
                    document.getElementById("location").innerHTML = "Location ke liye request time out ho gaya.";
                    break;
                case error.UNKNOWN_ERROR:
                    document.getElementById("location").innerHTML = "Ek unknown error ho gaya.";
                    break;
            }
        }
    </script>
</body>
</html>
