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
For ***sio-aro-ropp_f90*** repository access, please contact:  
📧 **Dr. Jennifer Haase** (jhaase@ucsd.edu)  
🏫 **Professor of Geophysics, Scripps Institution of Oceanography, University of California, San Diego**  
🔬 **Principal Investigator for Airborne Radio Occultation (ARO)**  

---

## **3. Contents of the sio-aro-ropp-f90 Repository**  

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
🔗 [ARO Converter to IODA](https://github.com/jhaaseresearch/aro-converter2ioda) *(Pending incorporation into JEDI)*  

### **Using ARO-Modified ROPP with MPAS-JEDI**  
For integrating the **ARO-modified ROPP** with **MPAS-JEDI**, refer to the following repository:  
🔗 [MPAS-Bundle Repository](https://github.com/JCSDA-internal/mpas-bundle/tree/release/2.1.0)  

For access, please contact the **Joint Center for Satellite Data Assimilation (JCSDA).**  

---

## **5. References**  

📄 **Hordyniec P., Haase J.S., Murphy M.J. Jr, Cao B., Wilson A.M.**  
*Forward modeling of bending angles with a two-dimensional operator for GNSS airborne radio occultations in atmospheric rivers.*  
**Journal of Advances in Modeling Earth Systems (JAMES), Submitted, 2024.**  

📄 **Phuong-Nghi Do, J. S. Haase, I. H. Banos, P. Hordyniec, B. Cao**  
*Impact of Airborne Radio Occultation Observations on Short Term Precipitation Forecasts of an Atmospheric River.*  
**Geophysical Research Letters [preprint], Submitted, 2025.**  
