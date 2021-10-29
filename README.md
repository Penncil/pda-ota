Tutorial for PDA-OTA
==============================================


<!---## Responsibilities for lead and participating sites--->
<!---![](pipeline.png)--->


## How to run PDA-OTA?

|          | Lead site                                | Participating site               |
|----------|------------------------------------------|----------------------------------|
| Step 0   | project proposal (e.g. [DLMM](https://drive.google.com/file/d/1hcvmoQe8jweaWOE7robNn2GkroYI9d24/view)) | project proposal                 |
| Step 1   | [sign up account](https://github.com/Penncil/pda-ota#step-1-sign-up-account) if not yet |       |
|          | [create new project](https://github.com/Penncil/pda-ota#create-new-project) |                            |
|          | invite Participating site to join |    | 
|          |                                          | [join project](https://github.com/Penncil/pda-ota#join-a-project), [sign up account](https://github.com/Penncil/pda-ota#step-1-sign-up-account) if not yet|
| Step 2.1 | [create control file](https://github.com/Penncil/pda-ota#step-21-create-control-file-lead-site) |                                 |
| Step 2.2 | [upload control file](https://github.com/Penncil/pda-ota#step-22-upload-control-file-lead-site) |                               |
| Step 2.3 |                                        | [download control file](https://github.com/Penncil/pda-ota#step-23-download-control-file-collborating-site)            |
| Step 2.4 |                                       | [run pda() in R to get aggregated data](https://github.com/Penncil/pda-ota#step-24-run-pda-collborating-site) |
| Step 2.5 |                                      | [upload aggregated data](https://github.com/Penncil/pda-ota#step-25-upload-aggregated-ata-participating-site)           |
| Step 2.6 | [download aggregated data](https://github.com/Penncil/pda-ota#step-26-download-aggregated-data-lead-site)  from all sites |                              |
| Step 2.7 | [run pda() in R to perform intermediate analysis](https://github.com/Penncil/pda-ota#step-27-run-pda-lead-site) |                            |
|          | run pda() in R to [update control file](https://github.com/Penncil/pda-ota#step-27-run-pda-lead-site)   |         |
|          | iterate Steps 2.2 - 2.7                   |     iterate Steps 2.3 - 2.5           |
| Step 3   | [run pda() get final results](https://github.com/Penncil/pda-ota#step-3-final-results-lead-site)              |                                  |
|          | Close project                            |                                  |


## Detailed instructions

### Step 1: Sign up account

Link to sign up account: https://pda-ota.pdamethods.org/login

#### Create new project

For lead site, create new project by clicking "+New project".

#### Join a project

For participating site, join new project by clicking "+Join project". (NOTE: To join an exising project, project ID and title are required, which can be found in the invite email or please contact the lead site for these information.)

------------------------

### Step 2.1: Create control file (lead site)


1. Install pda package, further instructions can be found here: https://github.com/Penncil/pda#how-to-install-the-pda-package.
2. Create control file:

```r
control <- list(project_name = 'Lung cancer study',
                step = 'initialize',
                sites = '<lead site name, participating site 1, participating site 2, etc>',
                heterogeneity = FALSE,
                model = '<model name, e.g., ODAL, ODAC, dPQL>',
                family = 'binomial',
                outcome = "status",
                variables = '<e.g., c('age', 'sex')>',
                optim_maxit = 100,
                lead_site = '<lead site name>',
                upload_date = as.character(Sys.time()) )

## run in local directory:
## dir can be set up to any directory with path instead of using getwd(), which is the current working directory. 
pda(site_id = '<lead site name>', control = control, dir = getwd())
``` 


------------------------

### Step 2.2: Upload control file (lead site)

Please upload the control.json file from Step 3.1 on pda-ota website in your project.


------------------------


### Step 2.3: Download control file (collborating site)

Please login to pda-ota website and download the control.json file in your project.


------------------------


### Step 2.4: Run pda() (Collborating site)

To get aggregated data, please run:

```r
pda(site_id = '<participating site 1>', ipdata = <input data>, dir=getwd())
```

Note: please install pda() package (instructions can be found [here](https://github.com/Penncil/pda#how-to-install-the-pda-package.)) before run the code above.


------------------------


### Step 2.5: Upload aggregated ata (participating site)

Please upload the aggregated data on pda-ota website in your project.


------------------------

### Step 2.6: Download aggregated data (Lead site)

Please download aggregated data uploaded data by all participating sites.

------------------------


### Step 2.7: Run pda() (Lead site)

To perform intermediate analysis and update control file, please run the following R code:

```r
pda(site_id = '<lead site name>', ipdata = <input data>, dir=getwd())
```
NOTE: to confirm if the control file is updated, please check the "step" status in your control.json. 

------------------------

### Step 3: Final results (Lead site)

To get final results, please see the final estimation .json file or run the following R code:

```r
config <- getCloudConfig(site_id = '<lead site name>', dir=getwd())
results <- pdaGet(name = '<.json file name>', config = config)
```


