---
description: Securely uploading files to the server
---

# File upload

### Recommendations <a id="&#x420;&#x435;&#x43A;&#x43E;&#x43C;&#x435;&#x43D;&#x434;&#x430;&#x446;&#x438;&#x438;"></a>

1. On the Back-end server use random filename instead of user given name .
2. Use whitelists for symbols in filenames. 
3. If it's not possible, clean out the filename from special symbols. In particular, from [RLO](https://xakep.ru/2018/02/13/telegram-rlo/).
4. Use only whitelists for checks on file extensions.
5. For creating whitelist use the following table:

| Mime types | Extensions | [Magic bytes](https://www.filesignatures.net/index.php?page=all) |
| :--- | :--- | :--- |
| image/jpeg | .jpeg/.jpg | FF D8 FF E0 |

1. All client side checks must be duplicated on server side.
2. Store files outside application root folder.
3. Remove the ability to run files from the filesystem. 

### Validation of extension: <a id="&#x412;&#x430;&#x43B;&#x438;&#x434;&#x430;&#x446;&#x438;&#x44F;-&#x440;&#x430;&#x441;&#x448;&#x438;&#x440;&#x435;&#x43D;&#x438;&#x44F;:"></a>

* Extension is included in the list of allowed extensions regardless of register.  
*  Mime-type is included in the allowed extensions list \(if your application accepts mime-type = octet-stream, proceed to the next checks\)
*  Binary file header is included into the allowed file formats.
*  Extension, mime-type and binary header are belong to same file type.
*  The file size does not exceed the allowed size.



