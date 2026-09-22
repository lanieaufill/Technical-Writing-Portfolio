<style>
  body {
    background-color: #C1E1C1 !important; 
  }
  .container-lg, .wrapper, main, .page-content {
    background-color: #ffffff !important;
    padding: 40px !important;
    border-radius: 12px !important;
    box-shadow: 0px 4px 20px rgba(0, 0, 0, 0.05) !important;
    margin-top: 30px !important;
    margin-bottom: 30px !important;
  }
</style>

# Installing your 3D Printer on Cura LulzBot Software

**Assumptions**

* You have correctly downloaded the **Cura Software** with the appropriate user settings.
* If you are using a **Cura Lulzbot printer**, then you can utilize the quick start guide and select your specific printer.
* If you are using a personal printer and hardware, then you should only have to set up the printer during the initial installation while downloading the software.

## Who is this for?

* Administrators that do not have access to allow the Cura software to edit the hard drive of their computer. 
* If this is the case, make sure to utilize these steps for printer installation with ***each reboot of the software***.

## Steps for adding your printer

1. Connect your 3D printer to your laptop or desktop computer with the cord provided with your printer
   * This is usually a **Type 2.0 USB A** to a **Type 2.0 USB B cable**.
3. Open the Cura LulzBot Software.
4. Click `Preferences`
5. Click `Configure Cura`
6. Click `Printers`
7. Locate your printer name and click.
8. Click `Add New`
9. Note- If you are not using a Cura Lulzbot Printer, then you will not locate the printer name among the list provided. Complete the following steps, or skip to step 10 if this does ot apply to you.
    * Click `Custom`.
    * Click `Custom FDM` or `Custom FFF` printer based on the make and model of your printer.
    * Rename the file type to match that of your printer make and model. 
    * Add your printer specifications under both the `Printer` tab and the `Extruder` tab
      * Printer Tab- input the exact **X,Y, and Z** planes of your printer bed.
      * Extruder Tab- input the **nozzle size**, in **mm**, and the compatible materials dimension.
    * If you followed this set of steps, you have successfully added your printer, and you can start printing
10. Click `Update Firmware` to upgrade your printer to the most current version of the firmware available. 
11. Click `Automatically Update`.
12. You have successfully added your Cura printer.
