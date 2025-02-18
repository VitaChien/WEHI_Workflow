## How to run Nextflow on Seqera on Milton HPC?  
### Step 1: Submit tickets to ask for access to Milton HPC and Seqera
For Milton, submit the [HPC Access Request](https://support.wehi.edu.au/support/catalog/items/134). And for Seqera, submit the [Seqera Platform Access Form](https://support.wehi.edu.au/support/catalog/items/151).
### Step 2: Upload raw data to `/vast/scratch/users/yourname/` + any subfolder you desire
1. Use [onDemand portal](https://ondemand.hpc.wehi.edu.au/pun/sys/dashboard) to upload the raw data.
2. Go to "Files" -> Vast -> the subfolder you want to upload the files to -> upload
  <img src="https://github.com/VitaChien/WEHI_Workflow/blob/update/nextflow-tutorial/screenshots/nextflow/%E6%88%AA%E5%9C%96%202025-02-18%20%E4%B8%8A%E5%8D%8811.49.45.png" width="300" height="225">
### Step 3: Generate access token on Seqera and fill it in the Nextflow Tower Agent page
1. Log in to [Seqera](https://seqera.services.biocommons.org.au/)
2. Go to the user icon on the upper right -> User tokens -> add Token
  <img src="https://github.com/VitaChien/WEHI_Workflow/blob/update/nextflow-tutorial/screenshots/nextflow/%E6%88%AA%E5%9C%96%202025-02-18%20%E4%B8%8A%E5%8D%8811.13.50.png" width="200" height="350">
  <img src="https://github.com/VitaChien/WEHI_Workflow/blob/update/nextflow-tutorial/screenshots/nextflow/%E6%88%AA%E5%9C%96%202025-02-18%20%E4%B8%8A%E5%8D%8811.13.57.png" width="500" height="100">
  <img src="https://github.com/VitaChien/WEHI_Workflow/blob/update/nextflow-tutorial/screenshots/nextflow/%E6%88%AA%E5%9C%96%202025-02-18%20%E4%B8%8A%E5%8D%8811.14.03.png" width="500" height="130">
3. Copy the token generated and paste it to the Nextflow Tower Agent at onDemand
  <img src="https://github.com/VitaChien/WEHI_Workflow/blob/update/nextflow-tutorial/screenshots/nextflow/%E6%88%AA%E5%9C%96%202025-02-18%20%E4%B8%8A%E5%8D%8811.13.50.png" width="200" height="350">
  
### Step 4: Select `Sarek_344` from Lanchpad and launch it
### Step 5: Fill in Run setup configuration and lanch the pipeline
