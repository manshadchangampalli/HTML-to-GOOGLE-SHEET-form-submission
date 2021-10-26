# HTML-to-GOOGLE-SHEET-form-submission
HTML to GOOGLE SHEET form submission code check the readme


step 1

  create a form and wrap it in  form tag
  
step 2 
  
  add the name attribute for all input and the form tag also and from method is "post"
step 3
  
  add the submit button type= submit
  
  
  
                          <form method="POST" autocomplete="off" name="manshad-contact-sheet" class="form">
                                    <p class="success">Thank you for your time today : )</p>
                                    <p class="error">Thank you for your time today. but message is not sended</p>
                                    <input placeholder="Name" name="name" type="text" required>
                                    <textarea placeholder="Message..." name="message" id="" cols="30" rows="10" required></textarea>
                                    <button type="submit" name="submit" class="send-icon-div">
                                            <h3>send</h3>
                                            <img class="send-icon" src="SVG/send icon (1).svg" alt="">
                                    </button>
                                    </div>
                                </form>
                                
                                
  step 3 
  
     # add the script 
         <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.2.1/jquery.min.js"></script>//in your html

     
     const scriptURL = 'https://script.google.com/macros/s/AKfycbxBh-oAKO9UoUQ1k1o24LJORtqe9Z_Om8PGQvS68YlLHPEMmamdzAFPRunKDdaK1C8oWA/exec'
     const form = document.forms['manshad-contact-sheet']//here your form name
     
     
    form.addEventListener('submit',e =>{
    e.preventDefault()
    fetch(scriptURL,{method:'POST',body: new FormData(form)})
    .then(response=> {success.style.display="block"
            setTimeout(()=>{
                Name.value= ""
                Name.placeholder="name"
                Message.value= ""
                success.style.display="none"

            },2000)
            
        })
    .catch((error) => {
        console.error('Error!',error.message)
        errorMsg.style.display="block" 
    }
    )
    
})


  step 4
  
    go to your google sheet create a sheet and the first line give the name attributes
    
    
  step 5 
  
    go to tools -> script editr -> add a file ->>add the name as the form name
    
    and peste the code
    
      var sheetName = 'Sheet1'
		var scriptProp = PropertiesService.getScriptProperties()

		function intialSetup () {
		  var activeSpreadsheet = SpreadsheetApp.getActiveSpreadsheet()
		  scriptProp.setProperty('key', activeSpreadsheet.getId())
		}

		function doPost (e) {
		  var lock = LockService.getScriptLock()
		  lock.tryLock(10000)

		  try {
			var doc = SpreadsheetApp.openById(scriptProp.getProperty('key'))
			var sheet = doc.getSheetByName(sheetName)

			var headers = sheet.getRange(1, 1, 1, sheet.getLastColumn()).getValues()[0]
			var nextRow = sheet.getLastRow() + 1

			var newRow = headers.map(function(header) {
			  return header === 'timestamp' ? new Date() : e.parameter[header]
			})

			sheet.getRange(nextRow, 1, 1, newRow.length).setValues([newRow])

			return ContentService
			  .createTextOutput(JSON.stringify({ 'result': 'success', 'row': nextRow }))
			  .setMimeType(ContentService.MimeType.JSON)
		  }

		  catch (e) {
			return ContentService
			  .createTextOutput(JSON.stringify({ 'result': 'error', 'error': e }))
			  .setMimeType(ContentService.MimeType.JSON)
		  }

		  finally {
			lock.releaseLock()
		  }
		}
    
    
    
    
 ........
 finished
 
