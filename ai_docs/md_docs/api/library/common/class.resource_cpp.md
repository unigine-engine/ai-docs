# Unigine::Resource Class (CPP)

**Header:** #include <UnigineResource.h>


Unigine *Resource* class.


This class allows you load and save data to the binary. In that case, the resource will be inside the binary, therefore platform independent. You can save to resources images, shaders or other content, that will be packed.


## Resource Class

### Members

---

## unsigned char * load ( const char *[] data )

Loads resource from ascii (base64) string.
### Arguments

- *const char *[]* **data** - Encoded resource ascii string.

### Return value

Pointer to the decoded data (null-terminated).
## unsigned char * load ( const char *[] data , int & size )

Loads resource from ascii string.
### Arguments

- *const char *[]* **data** - Encoded resource ascii (base64) string.
- *int &* **size** - The size of decoded data.

### Return value

Pointer to the decoded data (null-terminated).
## const char * save ( const char * name , const unsigned char * data , int size )

Saves data into the ascii (base64) string.
### Arguments

- *const char ** **name** - The name of resource.
- *const unsigned char ** **data** - The resource data.
- *int* **size** - The resource size.

### Return value

Encoded resource ascii (base64) string.
