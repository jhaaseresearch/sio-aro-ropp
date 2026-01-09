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

---

## **5. References**  

📄 **Hordyniec P., Haase J.S., Murphy M.J. Jr, Cao B., Wilson A.M., Banos, I.H.**  
*Forward modeling of bending angles with a two-dimensional operator for GNSS airborne radio occultations in atmospheric rivers.*  
**Journal of Advances in Modeling Earth Systems, 17, e2024MS004324. https://doi.org/10.1029/2024MS004324**  

📄 **Do, P.-N., Haase, J. S., Banos, I. H., Hordyniec, P., Cao, B.**  
*Impact of airborne radio occultation observations on short term precipitation forecasts of an atmospheric river.*  
**Geophysical Research Letters, 52, e2025GL115639. https://doi.org/10.1029/2025GL115639**  
