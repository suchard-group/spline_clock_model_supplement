# Smoothly Time-Varying Continuous Time Markov Chains in Phylogenetics

This repository contains the instructions and files to reproduce the analyses 
performed in the paper "Smoothly Time-Varying Continuous Time Markov Chains in 
Phylogenetics" by Datta et al. (2026).

### Setting up BEAGLE
Please follow the [BEAGLE installation instructions](https://github.com/beagle-dev/beagle-lib/wiki/MacInstallInstructions)
for Mac users and get the `hmc-clock` branch or run the commands below.

This will compile the CPU version of BEAGLE.
Follow the [instructions](https://github.com/beagle-dev/beagle-lib/wiki/MacInstallInstructions) if you need to install any other dependent software.

```
xcode-select --install
brew install cmake
git clone -b hmc-clock https://github.com/beagle-dev/beagle-lib.git
cd beagle-lib
mkdir build
cd build
cmake -DBUILD_CUDA=OFF -DBUILD_OPENCL=OFF -DBUILD_OPENMP=off ..
cmake --build .
sudo cmake --install .
```

For Linux users, the instructions can be found [here](https://github.com/beagle-dev/beagle-lib/wiki/LinuxInstallInstructions)

For Windows users, the instructions can be found [here](https://github.com/beagle-dev/beagle-lib/wiki/WindowsInstallInstructions)


The libraries are installed into `/usr/local/lib`.
You can find them by `ls /usr/local/lib/*beagle*`.


### Setting up BEAST

The following commands will compile the `hmc-clock` branch of BEAST.

```
git clone -b hmc-clock https://github.com/beast-dev/beast-mcmc.git
cd beast-mcmc
ant
```

For Mac users, you may need to install ant by `brew install ant` through [Homebrew](https://brew.sh/).

For Linux users, you can install ant by `sudo apt-get install ant`.

This will compile the `jar` files under `beast-mcmc/build/dist/` where you can find `beast.jar`, `beauti.jar` and `trace.jar`.

### Reproducing the analyses

You may use the following commands to run the analyses described in the manuscript.

Change your working directory to where you want to store the resulting log files first.

```
cd where_you_want_to_save_results
```

#### Piecewise Log-linear Rate with Initial Increase followed by Crash Simulation


* Fit uncorrelated relaxed clock (UCLD)

	```
	java -jar -Djava.library.path=/usr/local/lib where_beast_is_git_cloned/beast-mcmc/build/dist/beast.jar -seed 1161 -overwrite where_this_repository_is_stored/spline_clock_model_supplement/bilinear/bilinear_ucld.xml
	```
	
* Fit polyepoch clock model

	```
	java -jar -Djava.library.path=/usr/local/lib where_beast_is_git_cloned/beast-mcmc/build/dist/beast.jar -seed 1161 -overwrite where_this_repository_is_stored/spline_clock_model_supplement/bilinear/bilinear_pcm.xml
	```	
	
* Fit spline clock model (exponential link)

	```
	java -jar -Djava.library.path=/usr/local/lib where_beast_is_git_cloned/beast-mcmc/build/dist/beast.jar -seed 1161 -overwrite where_this_repository_is_stored/spline_clock_model_supplement/bilinear/bilinear_scm.xml
	```		

* Fit spline clock model (squared link)

	```
	java -jar -Djava.library.path=/usr/local/lib where_beast_is_git_cloned/beast-mcmc/build/dist/beast.jar -seed 1161 -overwrite where_this_repository_is_stored/spline_clock_model_supplement/bilin_squared/bilin_squared.xml
	```		

	

#### Log Linear Rate Simulation

* Fit UCLD

	```
	java -jar -Djava.library.path=/usr/local/lib where_beast_is_git_cloned/beast-mcmc/build/dist/beast.jar -seed 1161 -overwrite where_this_repository_is_stored/spline_clock_model_supplement/linear/linear_ucld.xml
	```
	
* Fit polyepoch clock model

	```
	java -jar -Djava.library.path=/usr/local/lib where_beast_is_git_cloned/beast-mcmc/build/dist/beast.jar -seed 1161 -overwrite where_this_repository_is_stored/spline_clock_model_supplement/linear/linear_pcm.xml
	```	
	
* Fit spline clock model (exponential link)

	```
	java -jar -Djava.library.path=/usr/local/lib where_beast_is_git_cloned/beast-mcmc/build/dist/beast.jar -seed 1161 -overwrite where_this_repository_is_stored/spline_clock_model_supplement/linear/linear_scm.xml
	```		

#### Constant Rate Simulation

* Fit UCLD

	```
	java -jar -Djava.library.path=/usr/local/lib where_beast_is_git_cloned/beast-mcmc/build/dist/beast.jar -seed 1161 -overwrite where_this_repository_is_stored/spline_clock_model_supplement/constant/constant_ucld.xml
	```
	
* Fit polyepoch clock model

	```
	java -jar -Djava.library.path=/usr/local/lib where_beast_is_git_cloned/beast-mcmc/build/dist/beast.jar -seed 1161 -overwrite where_this_repository_is_stored/spline_clock_model_supplement/constant/constant_pcm.xml
	```	
	
* Fit spline clock model (exponential link)

	```
	java -jar -Djava.library.path=/usr/local/lib where_beast_is_git_cloned/beast-mcmc/build/dist/beast.jar -seed 1161 -overwrite where_this_repository_is_stored/spline_clock_model_supplement/constant/constant_scm.xml
	```		
	



#### Foamy Virus

* Fit spline clock model with exponential link

	```
	java -jar -Djava.library.path=/usr/local/lib where_beast_is_git_cloned/beast-mcmc/build/dist/beast.jar -seed 1161 -overwrite where_this_repository_is_stored/spline_clock_model_supplement/fv/fv.xml
	```
	

#### SARS-COV-2


* Fit spline clock model with exponential link: requires genome data from GISAID.org to run sc2.xml

	```
	java -jar -Djava.library.path=/usr/local/lib where_beast_is_git_cloned/beast-mcmc/build/dist/beast.jar -seed 1161 -overwrite where_this_repository_is_stored/spline_clock_model_supplement/sc2/sc2.xml
	```
	
