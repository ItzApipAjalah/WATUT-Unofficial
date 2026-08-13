# WATUT (What Are They Up To) - 1.21.11 Fork

Note: This is a fork of the original [WATUT](https://github.com/Corosauce/WATUT) mod, specifically updated and ported to support Minecraft version 1.21.11.

## Build Instructions (Fabric)

To build the Fabric version of this mod, you will need the corresponding version of the `coroutil` library available locally.

### 1. Build CoroUtil
First, you need to build the `coroutil` library and obtain its Fabric jar. You can find the 1.21.11 fork here: [coroutil-unofficial](https://github.com/ItzApipAjalah/coroutil-unofficial).
1. Clone and navigate to your `coroutil-unofficial` project directory.
2. Run the build command for Fabric:
   ```bash
   ./gradlew build -b build_fabric.gradle
   ```
3. Locate the built jar file, which is typically found at `build/libs/coroutil-fabric-1.21.11-x.x.x.jar`.

### 2. Prepare the WATUT Project
1. In the root directory of this WATUT project, create a folder named `libs` if it does not already exist.
2. Copy the `coroutil-fabric` jar you built in the previous step into this `libs` folder.

### 3. Build WATUT
Now you are ready to build the WATUT mod.
1. Open a terminal in the root directory of the WATUT project.
2. Run the following command to build the Fabric version:
   ```bash
   ./gradlew build -b build_fabric.gradle
   ```
3. Once the build finishes successfully, your compiled mod file will be located in `build/libs/watut-fabric-1.21.11-x.x.x.jar`.
