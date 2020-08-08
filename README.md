# robloxasset
A tool used to download assets directly from Roblox.

## Features:
### You can download:
- Clothing Templates
- Catalog Accessories
- Library Assets

### You can't download:
- Offsale/Private Assets (such as scripts)
- Games
- Avatar Models

## How to use it:
- Head over to [robloxasset.tk](https://robloxasset.tk/)
- Enter the Asset URL (e.g. https://www.roblox.com/catalog/1110654902/Example-Shirt)
- Select the Asset Type (e.g. Clothing)
- Press "Download Asset" and wait for it to download

## How does it work?
This has been made possible by using Roblox's [Asset API](https://www.roblox.com/asset/?id=)

Data retreival methods can vary depending on which Asset Type you select (i.e. Clothing, Models, Audio).

### For Clothing:
The website works by sending a GET request to the Asset API, along with the `id` parameter (which is in the Asset URL you provide).
The API then returns an XML document which contains the ShirtTemplate URL.
Data is then retrieved from that URL, and finally saves it as a PNG directly to your machine.
### Example:
If we were trying to download [this](https://www.roblox.com/catalog/1110654902/Example-Shirt) shirt,
the website would send a GET request to: https://www.roblox.com/asset/?id=1110654902.

This would then return:
```xml
<roblox xmlns:xmime="http://www.w3.org/2005/05/xmlmime" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="http://www.roblox.com/roblox.xsd" version="4">
  <External>null</External>
  <External>nil</External>
  <Item class="Shirt" referent="RBX0">
    <Properties>
      <Content name="ShirtTemplate">
        <url>http://www.roblox.com/asset/?id=1110654897</url>
      </Content>
      <string name="Name">Shirt</string>
      <bool name="archivable">true</bool>
    </Properties>
  </Item>
</roblox>
```
The script selects the XML Element called `<url>`, and retrieves the value (which is the ShirtTemplate URL).

Finally, data from that URL is downloaded and saved onto your machine as a PNG file.

### For Audio:
This Asset Type is less complicated, as it doesn't require the Asset API.
Instead, a GET request is sent directly to the Asset URL, and then it converts the returned HTML as a DOM Object.
Using Selectors, the script finds the first element with class: `MediaPlayerIcon`, which contains an attribute (called `data-mediathumb-url`)
with the Audio URL.

### For Models & other assets:
(This applies to anything else on the library, and accessories.)

Uses same method as Clothing Templates, however saves the file as a RBXM (which can be opened directly in Roblox Studio).

## Disclaimer:
Do not redistribute assets that are not yours. I am not liable/responsible for any damage you may cause (i.e. Account Termination).
If you would like to avoid this, use RobloxAsset as a personal tool, and don't try to sell or make profit from anything you download.

RobloxAsset is not copyrighted nor a trademark, so feel free to use this tool in any projects you desire.
