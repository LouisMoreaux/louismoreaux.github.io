---
title: "Oracle APEX 20.2 and multipart/form-data"
last_modified_at: 2021-02-23T23:00:00+01:00
categories:
  - Oracle APEX
tags:
  - multipart/form-data
  - APEX
  - web service
---

Before APEX 20.2, APEX_WEB_SERVICE package didn’t support multipart/form-data. If like me, you had to reach a web service which accept only this type of request body, you had to use the ULT_HTTP package and create the body by yourself. Nick Buytaert made a good [post](https://apexplained.wordpress.com/2016/03/21/utl_http-and-a-multipartform-data-request-body/) about it on his blog post (which helped me a lot).

But thanks to the APEX Team, the [APEX_WEB_SERVICE](https://docs.oracle.com/en/database/oracle/application-express/20.2/aeapi/APEX_WEB_SERVICE.html) package in release 20.2 introduce the support of multipart/form-data. The creation of this type of body have never been so simple.

```sql
declare
    l_multipart apex_web_service.t_multipart_parts;
    l_blob blob;
    l_body blob;
begin
    select blob_column 
    into l_blob
    from my_file_table
    where id = 1;
    
    apex_web_service.append_to_multipart(
        p_multipart    => l_multipart,
        p_name         => 'file',
        p_content_type => 'application/octet-stream',
        p_body_blob    => l_blob
    );
        
    l_body := apex_web_service.generate_request_body(
        p_multipart => l_multipart
    );
    
    l_response := apex_web_service.make_rest_request(
    	p_url => 'https://...',
        p_http_method => 'POST',
        p_body_blob => l_body
    );
end;
```
The body sent with a simple text file is:

```
--A8BEA21E96C5B912
Content-Disposition: form-data; name="file"
Content-Type: application/octet-stream

This is a simple text file.
--A8BEA21E96C5B912--
```