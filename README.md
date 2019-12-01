# xCP 16.4 Documents (msw12) Rendition (JPEG Low Resolution) Quality!

Hi! 👋 If you wish to improve image (JPEG) quality of the MS Document's renditions (StoryBoards) while viewing in xCP Content Viewer, no worries! I'd suggest to follow this simple article. If you have got another option, please do comment!

I'm assuming that you have got a healthy CTS (Content Transformation Services) running and is 16.4 (or latest!). Also, you have little more storage to hold little big rendition in place of quality!

I also assume that your xCP Import Functionality is already working and producing poor JPEG renditions, which when user view in the xCP Viewer, feel bad about xCP2!

This is a tweaked version of the below OpenText Knowledge Base Article:
https://knowledge.opentext.com/knowledge/cs.dll/kcs/kbarticle/view/KB13494401 

## Applies to
Documentum Content Transformation Services - Documents 16.4
Documentum xCP 16.4

## Summary
In Documentum xCP, when you preview a document on xCP viewer the generated rendition quality is poor hence it looks blurry. The print out quality is cropped and fuzzy.
This issue occurs in (but may not be limited to):
Documentum xCP 16.4 and Content Transformation Service 16.4

## Update Transformation Profile 
1. Download and apply Documentum Content Transformation Service 16.4 patch14 or latest.

2. Checkout pdf_processing_xcp.xml in the /Media Server/System Profile/ via Documentum Administrator.
- Make the following changes under **storyboard_pdfstoryboard** section.
- Update doc_token_width value to 1280
- Update doc_token_height value to 1280
- Update doc_token_dpi value to 196
- Change doc_token_img_quality value from **regular** to **hires**
```
<InnerProfile path="/System/Media Server/System Profiles/storyboard_pdfstoryboard" waitOnCompletion="true" useTargetFormat="true">
<InnerTokenMapping LocalProfileToken="jpeg_lres" InnerProfileToken="doc_token_targetFormat" Literal="true"/>
<InnerTokenMapping Literal="true" InnerProfileToken="add_rendition_properties" LocalProfileToken="false"/>
<InnerTokenMapping LocalProfileToken="1500" InnerProfileToken="doc_token_width" Literal="true"/>
<InnerTokenMapping LocalProfileToken="1500" InnerProfileToken="doc_token_height" Literal="true"/>
<InnerTokenMapping LocalProfileToken="296" InnerProfileToken="doc_token_dpi" Literal="true"/>
<InnerTokenMapping LocalProfileToken="-1" InnerProfileToken="doc_token_pageNumber" Literal="true"/>
<InnerTokenMapping LocalProfileToken="true" InnerProfileToken="enable_activepreview" Literal="true"/>
<InnerTokenMapping LocalProfileToken="true" InnerProfileToken="zip_output" Literal="true"/>
<InnerTokenMapping Literal="true" InnerProfileToken="doc_token_colorSpace" LocalProfileToken="RGB"/>
<InnerTokenMapping Literal="true" InnerProfileToken="doc_token_colorProfile" LocalProfileToken="_use_default"/>
<InnerTokenMapping LocalProfileToken="hires" InnerProfileToken="doc_token_img_quality" Literal="true"/>
<InnerTokenMapping LocalProfileToken="10" InnerProfileToken="doc_token_chunksize" Literal="true"/>
</InnerProfile>
```
- Checkin the xml back to the same folder path

3. Checkout storyboard_pdfstoryboard (system profiles), you need to swap the sequences of the commands. 
- Change to load IMAGE3 first and then followed by PDFStoryboard (by default PDFStoryboard plugin load first).
```
<CommandFilePath mptype="IMAGE3">
/System/Media Server/Command Line Files/storyboard_pdf_imw.xml
</CommandFilePath>
<CommandFilePath mptype="PDFStoryboard">
/System/Media Server/Command Line Files/storyboard_pdfstoryboard.xml
</CommandFilePath>
```
- Checkin the xml profile

Out of the box plugin and configuration satisfy the basic need where the preview screen is small like D2 or Webtop however xCP viewer provides larger preview screen hence you require to adjust the setting to make the preview resolution looks sharp and clear.

## Don't Forget to Restart/Refresh CTS Services ✅ 
If you do not have access to CTS Server, don't be panic! Give below steps a go before bringing your Ring Master to the loop!

1. Go to DA Content Transformation Services Node
2. Then Instances
3. Right Click on Instance you are using, and open the properties!
4. Thats it! I hope you know what to do next?
5. [Stop](http://localhost:8080/da/webcomponent/admin/cts/viewdetails.jsp# "Stop") |[Start](http://localhost:8080/da/webcomponent/admin/cts/viewdetails.jsp# "Start") |[Refresh](http://localhost:8080/da/webcomponent/admin/cts/viewdetails.jsp# "Refresh  ")
6. Give another .docx or other supported source formats a go and share your view.

## Supported Source Formats

ppt8, ppt8_slide, ppt8slideshow, ppt8_template, ppt12, ppt12_slide, ppt12slideshow, ppt12template, ppt14, ppt14_slide, ppt14slideshow, ppt14template, ppt8, ppt8_slide, ppt8slideshow, ppt8_template, ppt12, ppt12_slide, ppt12slideshow, ppt12template, ppt14, ppt14_slide, ppt14slideshow, ppt14template, msw8, msw8template, msw12, msw12template, msw14, msw14template, msw8, msw8template, msw12, msw12template, msw14, msw14template, ppt15, ppt15_slide, ppt15template, ppt15slideshow, msw15, msw15template, ppt15, ppt15_slide, ppt15template, ppt15slideshow, msw15, msw15template
