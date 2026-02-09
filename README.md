# **sio-aro-ropp (instructions only)**  

This repository provides instructions for obtaining and using the **modified ROPP 2D bending angle operator** for **Airborne Radio Occultation (ARO)** under the `sio-aro-ropp-f90` (source code) repository.  

## **1. Overview**  

The **ROPP 2D operator** is maintained and licensed by the **EUMETSAT Radio Occultation Meteorology Satellite Application Facility (ROM SAF)**. More details about ROPP can be found at:  
🔗 [ROM SAF ROPP Website](https://rom-saf.eumetsat.int/ropp/)  

To access the **ROPP code**, users must:  
1. **Register** at [ROM SAF Registration](https://rom-saf.eumetsat.int/registration.php).  
2. **Agree to the software license terms** (Free of charge).  
3. **Download the ROPP package** from [ROM SAF Downloads](https://rom-saf.eumetsat.int/ropp/files.php).  

---

## **2. Accessing the Modified ROPP 2D Bending Angle Operator for ARO**  

The **modified ROPP 2D bending angle operator** for **ARO observations** (which requires an ROPP license) is available here:  
🔗 [sio-aro-ropp-f90](https://github.com/jhaaseresearch/sio-aro-ropp-f90)  

### **Requesting Access**  
For repository access, please contact:  
📧 **Dr. Jennifer Haase** (jhaase@ucsd.edu)  
🏫 **Professor of Geophysics, Scripps Institution of Oceanography, University of California, San Diego**  
🔬 **Principal Investigator for Airborne Radio Occultation (ARO)**  

---

## **3. Contents of the sio-aro-ropp-f90 repository**  

The `sio-aro-ropp-f90` repository includes:  
- ✅ Modified subroutines for the **ARO forward operator**, **tangent linear**, and **adjoint code**.  
- ✅ Instructions on building the modified **ROPP code** within the **Joint Effort for Data Assimilation Integration (JEDI)** framework.  
- ✅ CMake files for **compiler flags, target dependencies, and package configurations** for JEDI.  

For more details on JEDI and CMake, refer to:  
- 🔗 [JEDI Documentation](https://jointcenterforsatellitedataassimilation-jedi-docs.readthedocs-hosted.com/)  
- 🔗 [CMake for JEDI](https://jointcenterforsatellitedataassimilation-jedi-docs.readthedocs-hosted.com/en/latest/inside/developer_tools/cmake.html)  

---

## **4. Additional Resources**  

### **ARO Data Converter for JEDI**  
The **JEDI IODA converter** to read and convert ARO data is available here:  
🔗 [ARO Converter to IODA](https://github.com/jhaaseresearch/aro-converter2ioda)  
*Note: This converter is also integrated into JEDI ioda-converters repository here:*  
🔗 [ioda-converters](https://github.com/JCSDA-internal/ioda-converters.git)

### **Using ARO-Modified ROPP with MPAS-JEDI**  
For integrating the **ARO-modified ROPP** with **MPAS-JEDI**, refer to the following repository:  
🔗 [MPAS-Bundle Repository](https://github.com/JCSDA/mpas-bundle/tree/release/3.0.2)  

For access, please contact the **Joint Center for Satellite Data Assimilation (JCSDA).**  

## **Building mpas-bundle V3.0.2 on derecho**
1)	Log into Derecho
ssh -Y username@derecho.hpc.ucar.edu

2)	Configure your github environment  
vi ~/.gitconfig
<pre>
[filter "lfs"]  
        clean = git-lfs clean -- %f  
        smudge = git-lfs smudge -- %f  
        process = git-lfs filter-process  
        required = true  
[credential]  
        helper = cache --timeout=3600  
        helper = store  
        helper = store  
[user]  
        name = username  
        email = username’s email  
</pre>
Or
\# Set your name  
git config --global user.name "Your Name"  
\# Set your email  
git config --global user.email "yourname@somewhere.something"  
\# Set credential helper with timeout  
git config --global credential.helper 'cache --timeout=3600'  

git config --global credential.helper store 

3)	Clone the mpas-bundle

Go (or create) to the folder where you want to build the repository

Clone the Repository  
git clone -b release/3.0.2 https://github.com/JCSDA/mpas-bundle.git ./mpas-bundle_v3.0.2

Note: It may be necessary to create a personal access token through github before cloning

4)	Set up your environment for building mpas-bundle
   
cd mpas_bundle_v3.0.2  
vi env-setup/gnu-derecho.sh

modify environment variables to desired environment

source env-setup/gnu-derecho.sh

WARNING: The environment provided with the bundle includes outdated and unsupported modules. It is necessary to upgrade to spack-stack-1.9.3 or newer or else the build will fail. 

5)	Modify CMakeList.txt for your purpose 

For DA ARO, need to get the sio-aro-ropp-ufo and ufo with aro merged in V3.0.2  
#ecbuild_bundle( PROJECT ropp-ufo  GIT "https://github.com/JCSDA-internal/ropp-test.git"   TAG 96a0397 )  
ecbuild_bundle( PROJECT sio-ropp-ufo GIT "https://github.com/jhaaseresearch/sio-aro-ropp-f90.git" BRANCH main 
UPDATE)

Turn ON or OFF double precision (ON for running the mpas-jedi test suite, OFF for MPAS-Workflow calculations when using the mpas-bundle build)  
set(MPAS_DOUBLE_PRECISION "ON" CACHE STRING "MPAS-Model: Use double precision 64-bit Floating point.")

6)  Create and navigate into the build directory
   
mkdir build  
cd build

7)	Configure the build using CMake

cmake ../

if python fails to build, run  
rm CMakeCache.txt (If it exists from a previous cmake command)  
cmake -DPython3_EXECUTABLE=$(which python3) ../

8)	Make sure ROPP_ARO "Using ROPP for airborne radio occultation"  is ON
    
vi ../ufo/CMakeLists.txt

9)	clear cached CMake and build ufo
    
cd ../build  
rm CMakeCache.txt  
cmake ../  

If python fails, specify path to python executable  
rm CMakeCache.txt  
cmake -DPython3_EXECUTABLE=$(which python3) ../  

10)	Use the run_make.bundle.sh script to generate a batch job for building.

Build bundle  
bash ../env-setup/run_make.bundle.sh -A <your_project_number> -c gnu -n  
qsub make.pbs.sh  

To give higher priority, add this command to the top of make.pbs.sh  
#PBS -l job_priority=premium

To check the job  
qstat -u username  
or vi mpas-make*   

You can also check the job continuously by typing  
tail -f mpas-make*  
It won’t necessarily tell you when it has finished, it will just exit the queue.  
If it exits the queue without any apparent error, try again.

11)	Generate a batch job for running mpas-jedi's test suite and submit it using qsub

bash ../env-setup/run_make.bundle.sh -A <your_project_number> -c gnu -x ctest -n  
qsub ctest.pbs.sh  
chmod u+x ../env-setup/run_make.bundle.sh (if Permission denied)  

Check progress  
tail -f mpas-ctest.*  
Check ctest log file in mpas-jedi/Testing/Temporary/LastTest.log

12)	Generate a batch job for running ufo's ARO test suite and submit it using qsub

cp ctest.pbs.sh ctest_aro.pbs.sh  
vi ctest_aro.pbs.sh and modify   
#cd mpas-jedi && ctest  
cd ufo && ctest -R gnssaro  
qsub ctest_aro.pbs.sh  
Check ctest log file in ufo/Testing/Temporary/LastTest.log  

13)	Compile single precision:

After passing all ctests go back to step 5 and in CMakeLists.txt set  
set(MPAS_DOUBLE_PRECISION "OFF" CACHE STRING "MPAS-Model: Use double precision 64-bit Floating point.")  

Then repeat steps 9 and 10 to complete installation

---

## **5. References**  

📄 **Hordyniec P., Haase J.S., Murphy M.J. Jr, Cao B., Wilson A.M., Banos, I.H.**  
*Forward modeling of bending angles with a two-dimensional operator for GNSS airborne radio occultations in atmospheric rivers.*  
**Journal of Advances in Modeling Earth Systems, 17, e2024MS004324. https://doi.org/10.1029/2024MS004324**  

📄 **Do, P.-N., Haase, J. S., Banos, I. H., Hordyniec, P., Cao, B.**  
*Impact of airborne radio occultation observations on short term precipitation forecasts of an atmospheric river.*  
**Geophysical Research Letters, 52, e2025GL115639. https://doi.org/10.1029/2025GL115639**  
