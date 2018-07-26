# Device-Component-Inventory
Custom CA PC app which displays device components with several attributes in a table view. The app
runs typically in a device context but can also be used in interface context.

# Use Case
This app provides a comprehensive view of the Data Aggregator attributes such as poll/filter/present status.

# Example
![App View Device Component Inventory Image]
(https://github.com/CA-PM/Device-Component-Inventory/images/devcominv.png)

If added to an interface context page it will only display a single line:
![App View Interface Context Inventory Image]
(https://github.com/CA-PM/Device-Component-Inventory/images/intcominv.png

# Approach
CA PC app with following characteristics
* uses DA REST calls to retrieve component information and component retired information
* uses CA PM OpenAPI to query interface specific attributes
* Uses DataTables graphics library
* Can live on device or interface context page
* The following component attributes are included:
  * DA component ID (in device context with hyperlink to the component context page)
  * Name
  * Description
  * Name Alias (interfaces)
  * Interface alias (interfaces)
  * Optional: custom attribute (interfaces)
  * OperStatus (interfaces)
  * Metric Family name
  * Vendor Cert name
  * IsPresent
  * IsFiltered
  * IsPolled
  * IsPollEnabled (v1.1)

# Prerequisites
v1.0 CA PM 3.5. The app retrieves the AlternateName for interfaces which is new to 3.5.
v1.1 CA PM 3.6. table allows multiple row selections (Ctrl+click) and change of "IsPollEnabled" flag.

# Installation
The app is packed in a ZIP archive and can be installed through CA PM 3.2+ App Deployment function.
1. Download the master zip archive on your workstation
2. extract DevCompInventory.zip
3. Under CA PC Administration -> App Deployment, select DevCompInventory.zip and install it.
4. Navigate e.g. to a device context page.
5. Add a context tab, name it e.g. Components
6. In page editor, select single column layout and create an App View (under External Links)
and select "Device Component Inventory" in the app drop down.
7. If needed, add any interface custom attribute as a parameter to the URL definition

## App view parameters:
### Default:
URL:
/pc/apps/user/DevCompInventory/DevCompInventory.html?id={ItemIdDA}&ItemTypeName={ItemTypeN
ame}&limit=1000
which consists of
- id={ItemIdDA} page context (device OR interface item ID DA)
- ItemTypeName={ItemTypeName} page context type
- limit=1000 query limit: the number of rows retrieved
- optionally, if a custom attribute is defined for interfaces:
o ca1=ConnectsTo custom attribute
o ca1Label=Connects To custom attribute label
Height: 600 default for device context
Height: 80 sufficient view height in interface context

### URL Example with custom attribute:
URL:/pc/apps/user/DevCompInventory/DevCompInventory.html?id={ItemIdDA}&limit=1000&ca1=Conne
ctsTo&ca1Label=Connects To

# Notes
The app is provided as an example and no warranties are provided or made
* Users other than admin need to be enabled for DA REST access in CA PC (see
https://communities.ca.com/docs/DOC-231174750-ca-pc-apps-and-user-authorization)
