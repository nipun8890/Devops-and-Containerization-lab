<!DOCTYPE html>
<html>
<head>
    <title>Experiment 2 - Docker</title>

    <style>
        body {
            font-family: Arial, sans-serif;
            background: #f4f6f8;
            margin: 0;
        }

        .navbar {
            background: #0d1117;
            color: white;
            padding: 15px;
            font-size: 18px;
        }

        .container {
            width: 80%;
            margin: 30px auto;
            background: white;
            padding: 25px;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
        }

        h1 { color: #1976d2; }
        h2 { border-bottom: 2px solid #ddd; padding-bottom: 5px; }

        img {
            width: 100%;
            margin-top: 15px;
            border-radius: 8px;
        }

        code {
            display: block;
            background: #eee;
            padding: 8px;
            border-radius: 5px;
            margin: 10px 0;
        }

        ul {
            line-height: 1.6;
        }
    </style>
</head>

<body>

<div class="navbar">Home</div>

<div class="container">

<h1>Experiment 2</h1>
<p><b>Docker Installation, Configuration, and Running Images</b></p>

<p>
<b>Name:</b> Nipun Agrawal <br>
<b>Roll No:</b> R2142230048 <br>
<b>SAP ID:</b> 500119472 <br>
<b>University:</b> UPES Dehradun
</p>

<h2>Aim</h2>
<p>
To install Docker, pull images, run containers, and manage container lifecycle.
</p>

<h2>Objectives</h2>
<ul>
<li>Pull Docker images from Docker Hub</li>
<li>Run containers with port mapping</li>
<li>Verify running containers</li>
<li>Manage container lifecycle</li>
</ul>

<h2>Theory</h2>
<p>
Docker is a containerization platform that packages applications with dependencies into containers.
Containers are lightweight and faster than virtual machines.
</p>

<p>
A <b>Docker Image</b> is a template. A <b>Docker Container</b> is a running instance of that image.
</p>

<h2>Software Requirements</h2>
<ul>
<li>Windows OS</li>
<li>Docker Desktop (WSL)</li>
<li>Ubuntu</li>
</ul>

<h2>Procedure</h2>

<h3>Step 1: Pull Docker Image</h3>
<img src="Screenshots/dockerpull.png">
<code>docker pull nginx</code>

<p>This downloads the Nginx image from Docker Hub.</p>

<h3>Step 2: Run Container</h3>
<img src="Screenshots/dockerrun.png">
<code>docker run -d -p 8080:80 nginx</code>

<p>
<b>-d</b> → Background mode <br>
<b>-p</b> → Port mapping <br>
</p>

<h3>Step 3: Verify Containers</h3>
<img src="Screenshots/dockerrun.nginx.png">
<img src="Screenshots/dockerps.png">
<code>docker ps</code>

<h3>Step 4: Stop & Remove Container</h3>
<img src="Screenshots/dockerstop.png">
<code>docker stop &lt;container_id&gt;</code>

<img src="Screenshots/dockerrm.png">
<code>docker rm &lt;container_id&gt;</code>

<h3>Step 5: Remove Image</h3>
<code>docker rmi nginx</code>

<p>This deletes the image and frees space.</p>

<h2>Result</h2>
<p>
Docker images were pulled, containers executed, and lifecycle commands were performed successfully.
</p>

<h2>Conclusion</h2>
<p>
Docker provides a lightweight and efficient environment for application deployment.
</p>

<h2>Viva Questions</h2>
<ul>
<li>What is a Docker image?</li>
<li>What is a container?</li>
<li>Difference between docker run and docker start?</li>
<li>Why port mapping is used?</li>
<li>Why containers are lightweight?</li>
</ul>

<h2>Overall Conclusion</h2>
<p>
Containers are faster and efficient for deployment, while VMs provide stronger isolation.
</p>

</div>

</body>
</html>