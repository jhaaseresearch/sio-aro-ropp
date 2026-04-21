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

## **5. Building mpas-bundle v3.0.2 on Derecho**

The steps below are a tested workflow for building MPAS-Bundle release `3.0.2` with ARO-related updates.

1. Log in to Derecho:

```bash
ssh -Y username@derecho.hpc.ucar.edu
```

2. Configure your GitHub identity and credentials:

```bash
git config --global user.name "Your Name"
git config --global user.email "yourname@somewhere.something"
git config --global credential.helper 'cache --timeout=3600'
git config --global credential.helper store
```

Optional: if you prefer editing `~/.gitconfig` directly, ensure your `user`, `credential`, and `lfs` settings are present and correct.

3. Clone `mpas-bundle` release `3.0.2` into a dedicated directory:

```bash
git clone -b release/3.0.2 https://github.com/JCSDA/mpas-bundle.git ./mpas-bundle_v3.0.2
```

Note: a GitHub personal access token may be required.

4. Set up the build environment:

```bash
cd mpas-bundle_v3.0.2
vi env-setup/gnu-derecho.sh
source env-setup/gnu-derecho.sh
```

Update environment variables in `env-setup/gnu-derecho.sh` as needed.

WARNING: The environment provided with the bundle may include outdated/unsupported modules. Upgrade to `spack-stack-1.9.3` or newer, or the build may fail.

5. Modify `CMakeLists.txt` for ARO DA use:

- Replace the default `ropp-ufo` bundle entry with the ARO-modified source, for example:

```cmake
# ecbuild_bundle( PROJECT ropp-ufo GIT "https://github.com/JCSDA-internal/ropp-test.git" TAG 96a0397 )
ecbuild_bundle( PROJECT sio-ropp-ufo GIT "https://github.com/jhaaseresearch/sio-aro-ropp-f90.git" BRANCH main UPDATE )
```

- Set precision mode based on workflow needs:

```cmake
set(MPAS_DOUBLE_PRECISION "ON" CACHE STRING "MPAS-Model: Use double precision 64-bit Floating point.")
```

Use `ON` for running the `mpas-jedi` test suite. Use `OFF` for MPAS-Workflow calculations with the bundle build.

6. Create and enter a build directory:

```bash
mkdir build
cd build
```

7. Configure with CMake:

```bash
cmake ../
```

If Python configuration fails:

```bash
rm -f CMakeCache.txt
cmake -DPython3_EXECUTABLE=$(which python3) ../
```

8. Verify `ROPP_ARO` (`Using ROPP for airborne radio occultation`) is `ON` in `ufo/CMakeLists.txt`.

9. Clear CMake cache and reconfigure (especially after changing CMake options):

```bash
cd ../build
rm -f CMakeCache.txt
cmake ../
```

If Python fails again, rerun with explicit `Python3_EXECUTABLE` as in Step 7.

10. Generate and submit the bundle build batch job:

```bash
bash ../env-setup/run_make.bundle.sh -A <your_project_number> -c gnu -n
qsub make.pbs.sh
```

Optional higher priority (add near top of `make.pbs.sh`):

```bash
#PBS -l job_priority=premium
```

Monitor build progress:

```bash
qstat -u username
tail -f mpas-make*
```

11. Generate and submit the `mpas-jedi` test suite job:

```bash
bash ../env-setup/run_make.bundle.sh -A <your_project_number> -c gnu -x ctest -n
qsub ctest.pbs.sh
```

If needed:

```bash
chmod u+x ../env-setup/run_make.bundle.sh
```

Monitor tests and logs:

```bash
tail -f mpas-ctest.*
```

`mpas-jedi` test log location:

```text
mpas-jedi/Testing/Temporary/LastTest.log
```

12. Generate and submit the `ufo` ARO test suite job:

```bash
cp ctest.pbs.sh ctest_aro.pbs.sh
vi ctest_aro.pbs.sh
```

In `ctest_aro.pbs.sh`, change:

```bash
# cd mpas-jedi && ctest
cd ufo && ctest -R gnssaro
```

Then submit:

```bash
qsub ctest_aro.pbs.sh
```

`ufo` test log location:

```text
ufo/Testing/Temporary/LastTest.log
```

13. Build single precision after tests pass:

In `CMakeLists.txt`, set:

```cmake
set(MPAS_DOUBLE_PRECISION "OFF" CACHE STRING "MPAS-Model: Use double precision 64-bit Floating point.")
```

Then repeat Steps 9 and 10 to complete the single-precision installation.

---

## **5. References**  

📄 **Hordyniec P., Haase J.S., Murphy M.J. Jr, Cao B., Wilson A.M., Banos, I.H.**  
*Forward modeling of bending angles with a two-dimensional operator for GNSS airborne radio occultations in atmospheric rivers.*  
**Journal of Advances in Modeling Earth Systems, 17, e2024MS004324. https://doi.org/10.1029/2024MS004324**  

📄 **Do, P.-N., Haase, J. S., Banos, I. H., Hordyniec, P., Cao, B.**  
*Impact of airborne radio occultation observations on short term precipitation forecasts of an atmospheric river.*  
**Geophysical Research Letters, 52, e2025GL115639. https://doi.org/10.1029/2025GL115639**  
