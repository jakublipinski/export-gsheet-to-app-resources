# Export data from Google Spreadsheet to iOS and Android resource text files

The project allows to Google Spreadsheet as main resource of the strings in the iOS and Android project. The script exports the texts from the spreadsheet to the Android and iOS specific resource files.

## Installing

```
git clone git@github.com:jakublipinski/export-gsheet-to-app-resources.git
cd export-gsheet-to-app-resources
python3 -m venv venv
source venv/bin/activate
python3 -m pip install -r requirements.txt
```

## Set up the spreadsheet

* Create a new Google Spreadsheet
* Create following columns in the first row:
    * `ID` column
    * 2-letter language code for each language you want to support
    * `Comment` column

You can create as many Sheets as you like. Keep the above structure in each of them. On Android each sheet will be exported to a separate file. On iOS all texts wlll be merged into one `Localizable.strings` file.

You can see an example of the spreadsheet [here](https://docs.google.com/spreadsheets/d/13yWCFwnb9ZJTy2LA8mN485_R8lcpOZpmvKhMxLoMON0/edit?usp=sharing)

## Setup a new Google Developer Project to get access to the sheet from the script

Note: you can do it once and reuse the credentials in each of your projects.

### Setup New Project

* Go to Google Developers Console - https://console.developers.google.com/
* Create a New project and provide its name e.g. `Sheets Reader`

### Enable Google Sheets API

* Ensure your newly created project is selected in the project dropdown
* Choose Library from the menu on the left
* Enter `sheet` into the Search Bar and choose Google Sheets API. Press Enable
 
### Create and Download Credentials

* Go to `Credentials`
* Choose `+Create Credentials` and select `Service account`
* Enter some Service account name e.g. `Sheet Reader Service`
* Click `Create`
* Click `Continue` in `Service account permissions (optional)` in the next prompt
* Click `+Create Key` and `JSON` as a key type. Download the .json file to your * project folder
* Click "Done"

## Share your spreadsheet with your service e-mail address

* Copy the email address shown under the Service Account list e.g `your-service-name@project-name-12345.iam.gserviceaccount.com`
* Share your spreadsheet with the email address. The view access is enough

## Export the Sheet to Android and iOS resource files

```
python export.py \
--credentials credentials_file.json \
--gsheet_key 13yWCFwnb9ZJTy2LA8mN485_R8lcpOZpmvKhMxLoMON0 \
--android_res res \
--ios_res ios
```

The parameters are:
`--credentials` - the credentials file downloaded from the Google Developer Console (.json)
`--gsheet_key` - the Google Spreadsheet key from its url
`--android_res` - the root folder of the Android resource files
`--ios_res` - the root folder of the iOS resource files


