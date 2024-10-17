  ## Cloud Native Buildpacks

### What is CNBs?
- The CNB project was initiated by Pivotal and Heroku in January 2018 and joined the Cloud Native Computing Foundation (CNCF) as an Apache-2.0 licensed project in October 2018.
- Cloud Native Buildpacks (CNBs) **transform your application source code into container images** that can run on any cloud.
- With buildpacks, organizations can concentrate the knowledge of container build best practices within a specialized team, **instead of having application developers across the organization individually maintain their own Dockerfiles**.
- This makes it easier to know what is inside application images, enforce security and compliance requirements, and perform upgrades with minimal effort and intervention.

#
### Why CNBs?
- Control - Balanced control between App Devs and Operators.
- Compliance - Ensure apps meet security and compliance requirements.
- Maintainability - Perform upgrades with minimal effort and intervention.

#### Features of CNBs:
- It auto-detects your code's programming language and its version
- Advanced Caching
- <mark>Images can be built directly from application source without additional instructions</mark>.
- Supports more than one programming language family.
- Image contains only what is necessary.
- Leverage production-ready buildpacks maintained by the community.

#### Working :
Here's an overview of how Cloud Native Buildpacks work:

- Detection: Buildpacks first detect the language and framework of the application based on the provided source code. They determine which buildpacks are needed, e.g., for Node.js, Java, Python, etc.
- Building: Once the appropriate buildpacks are chosen, they are used to assemble the container image. This involves installing necessary dependencies, configuring the application environment, and optimizing the image for performance and security.
- Packaging: The buildpacks package the application and its dependencies into an OCI-compliant container image. This image can then be deployed to platforms like Kubernetes or Docker.

#

#### Detailed Breakdown of Cloud Native Buildpacks:
1. Key Concepts and Components
- Buildpacks: These are modular scripts responsible for transforming code into container images. Each buildpack handles specific tasks like setting up runtime environments, configuring build tools, or installing dependencies.
- Lifecycle Phases: The lifecycle of CNBs involves distinct phases like detection, analysis, building, exporting, and caching, ensuring efficiency and incremental builds:
Detection: Buildpacks analyze your app to determine the required buildpacks based on the language or framework.
- Build: The necessary buildpacks are run, typically downloading dependencies (e.g., for Java, Node.js), configuring the environment, and preparing your app for execution.
- Export: After the build, the container image is created and optimized, following OCI (Open Container Initiative) standards.
- Stacks: These are pre-built layers that buildpacks use as a base, which typically includes the OS, libraries, and utilities necessary to run applications. Stacks allow applications to run on standardized environments.
- Builders: A combination of stacks and buildpacks, bundled to create the actual container image. They provide a base environment for different languages.
2. Cloud Native Buildpack Lifecycle
- Detection Phase: Buildpacks inspect your app to determine the suitable language runtime and dependencies. If a language is detected, the corresponding buildpacks are selected (e.g., Node.js buildpacks for JavaScript apps).
- Build Phase: Buildpacks compile and configure your app, installing dependencies, configuring environment variables, and preparing a production-ready version of your application.
- Layering & Reusability: Buildpacks create layers for each component of the build (runtime, dependencies, application code). This layered approach ensures that changes in one layer (e.g., app code) don’t require rebuilding all layers (like the runtime). This speeds up incremental builds.
- Caching: CNBs automatically handle caching dependencies and build artifacts, reducing build times by reusing previous layers where possible

#

### Deploy your application using Cloud Native Builpacks

#### Pre-requisites:

- AWS account
- An Ubuntu EC2 machine 
- Docker installed

#
#### Steps:
- Update your machine
```bash
sudo apt update
```
#
- Install docker
```bash
sudo apt install docker.io -y
```
#
- Provide permission to ubuntu user to docker group
```bash
sudo usermod -aG docker $USER && newgrp docker
```
#
- Install pack utility to build image
```bash
sudo add-apt-repository ppa:cncf-buildpacks/pack-cli
sudo apt-get update
sudo apt-get install pack-cli
```
#
- Clone your code
```bash
git clone https:<your code>.git
```
#

#
- Run the following command to get the pack builder
```bash
pack build suggest
```
#
- Copy the suggested google builder and paste in the below command
```bash
pack build --builder=<your-builder-from-above-command> <your image name>
```

#
- After build, check images
```bash
docker images
```
#
- Run the image as a container
```bash
docker run -itd --name nodeapp -p <map the respective port> <image name>
```
 you have deployed and application using Cloud Native Buildpacks.
