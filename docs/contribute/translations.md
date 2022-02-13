# Localisation of content

## Overview of translatable content

- Trains
- Tracks
- Libre Train Sim itself
    - Menus
    - In-game Messages
    - Tutorials

!!! warning

	We are planning to move *away* from CSV files. The past prove them to be hard to maintain. The content on this page is subjected to change but nonetheless relevant for 0.9.
	
	For 1.0 we plan to switch to a gettext based approach using a translation service like poeditor or weblate.

## Step by step guide

### Preparation

  1. A `.csv` editor like [Libre Office](https://www.libreoffice.org/download/download/) is recommended. (Microsoft Excel won't work)
  2. Get the latest [sources](https://github.com/Libre-TrainSim/Libre-TrainSim/archive/master.zip) either by clicking the link or by cloning the repository
  3. Download [Godot](https://godotengine.org/download)
  4. Extract both files
  5. Start Godot and scan in the repository folder
  6. Godot should have found Libre Train Sim. Double-click the entry to start the project
  7. Press `F5` to run Libre Train Sim

### Translation
Translations are stored using `.csv` files. Those files are found in:
 - `/src/Trains`
 - `/src/Translations`

The import and export settings should use `,` as separator and `"` as string separator. Libre Office default settings are fine. The file is encoded in `UTF-8`.

!!! Danger

	Earlier versions of the documentation declared the deletion of all columns except `keys` and `en` to be fine. However, this caused major headaches when we had to implement the files. So please, please, do not. Shrink or hide the columns instead.

Enter the desired [language code](https://docs.godotengine.org/en/stable/tutorials/i18n/locales.html) into the first line of your column. Currently, there is no need to use country specific language codes. Please stick to the generic locales instead. For example use `en` instead of `en_GB`.

!!! info

	The generic locale rule is in place to reduce the maintance burden. Every added translation needs to keep updated. If you feel like this rule discriminates against your language because there are significant differences, please raise an [issue on GitHub](https://github.com/Libre-TrainSim/Libre-TrainSim/issues/new).

You can enter new lines using `\n` and tabs using `\t`

Once you finished your file, save it with the same name as `.csv` file.

### Testing

1. Save the file as `.csv`
2. Start Godot and launch Libre Train Sim
3. Godot should automatically detect file changes.
4. Press `F5` and select your language in the settings.

## Contribute the translation

There are two options to contribute the changes back upstream. The preferred option is easy on our side using a [pull request](https://github.com/Libre-TrainSim/Libre-TrainSim/compare). The process will be described in the yet-to-be-written dedicated guide. The other option is to create a new [issue on GitHub](https://github.com/Libre-TrainSim/Libre-TrainSim/issues/new) with your changed files attached.
