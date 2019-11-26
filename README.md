# xCP 16.4 Documents (msw12) Rendition (JPEG Low Resolution) Quality!

Hi! 👋 If you wish to improve image (JPEG) quality of the MS Document's renditions (StoryBoards) while viewing in xCP Content Viewer, no worries! I'd suggest to follow this simple article. If you have got another option, please do comment!

I'm assuming that you have got a healthy CTS (Content Transformation Services) running and is 16.4 (or latest!). Also, you have little more storage to hold little big rendition in place of quality!

I also assume that your xCP Import Functionality is already working and producing poor JPEG renditions, which when user view in the xCP Viewer, feel bad about xCP2!

## Update Transformation Profile 

Right, lets start using DA and navigate to the file below. Please do not complaint if file is not visible as you forget to filter all the versions on the right hand top corner. 😊 

**File**: ``/System/Media Server/System Profiles/transformXcpDocumentDirect``

Replace the Content as suggested below (Checkout-Checking-Minor-Version):

**From**:
```
<CommandFilePath mptype="DOC6">
		/System/Media Server/Command Line Files/transformXcpDocument.xml
</CommandFilePath>	
```
**To**: 
```
<CommandFilePath mptype="IMAGE3">
		/System/Media Server/Command Line Files/transformTo_imw.xml
</CommandFilePath>
```
Well done! 👍 

## Don't Forget to Restart/Refresh CTS Services ✅ 
If you do not have access to CTS Server, don't be panic! Give below steps a go before bringing your Ring Master to the loop!

1. Go to DA Content Transformation Services Node
2. Then Instances
3. Right Click on Instance you are using, and open the properties!
4. Thats it! I hope you know what to do next?
5. [Stop](http://localhost:8080/da/webcomponent/admin/cts/viewdetails.jsp# "Stop") |[Start](http://localhost:8080/da/webcomponent/admin/cts/viewdetails.jsp# "Start") |[Refresh](http://localhost:8080/da/webcomponent/admin/cts/viewdetails.jsp# "Refresh  ")
6. Give another .docx or other supported source formats a go and share your view.

## Source Format

ppt8, ppt8_slide, ppt8slideshow, ppt8_template, ppt12, ppt12_slide, ppt12slideshow, ppt12template, ppt14, ppt14_slide, ppt14slideshow, ppt14template, ppt8, ppt8_slide, ppt8slideshow, ppt8_template, ppt12, ppt12_slide, ppt12slideshow, ppt12template, ppt14, ppt14_slide, ppt14slideshow, ppt14template, msw8, msw8template, msw12, msw12template, msw14, msw14template, msw8, msw8template, msw12, msw12template, msw14, msw14template, ppt15, ppt15_slide, ppt15template, ppt15slideshow, msw15, msw15template, ppt15, ppt15_slide, ppt15template, ppt15slideshow, msw15, msw15template
