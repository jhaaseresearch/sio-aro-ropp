# sio-aro-ropp
This repository contains instructions for how to obtain the modified ROPP 2D bending angle operator for ARO under the sio-ropp repository and its contents.

The ROPP 2D operator is maintained and licensed by the EUMETSAT Radio Occultation Meteorology Satellite Application Facility (ROM SAF) at https://rom-saf.eumetsat.int/ropp/. Users wishing to obtain the ROPP code will need to first register at this web site via the registration page https://rom-saf.eumetsat.int/registration.php and agree to the terms and conditions of the software licence. There is no charge for the package. Registered users should login and access the ROPP package from the download page https://rom-saf.eumetsat.int/ropp/files.php.


The modified ROPP 2D bending angle operator for ARO observation, which relies on access to a ROPP license is available at https://github.com/jhaaseresearch/sio-ropp. 

For access to the sio-ropp repository, users should contact Dr. Jennifer Haase (jhaase@ucsd.edu), Professor of Geophysics of the Scripps Institution of Oceanography of the University of California, San Diego and Principal Investigator for Airborne Radio Occultation (ARO).

The sio-ropp repository contains the modified subroutines for the ARO forward operator and its tangent linear and adjoint code, as well as information on how to build the modified ROPP code within the Joint Effort for Data Assimilation Integration (JEDI) framework https://jointcenterforsatellitedataassimilation-jedi-docs.readthedocs-hosted.com/. For building, testing and packaging, JEDI relies on Cmake [Cmake](https://cmake.org/). Therefore, files needed for the compiler flags, target dependencies, and packages are included in the sio-ropp repository. For more details about using Cmake in JEDI, please see https://jointcenterforsatellitedataassimilation-jedi-docs.readthedocs-hosted.com/en/latest/inside/developer_tools/cmake.html.

References:
Forward modeling of bending angles with a two-dimensional operator for GNSS airborne radio occultations in atmospheric rivers, Hordyniec P, Haase JS, Murphy MJ Jr, Cao B, Wilson AM., Journal of Advances in Modeling Earth Systems (JAMES), submitted, 2024.
