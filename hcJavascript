/*
 * jQuery v1.9.1 included
 */

$(document).ready(function() {

  // social share popups
  $(".share a").click(function(e) {
    e.preventDefault();
    window.open(this.href, "", "height = 500, width = 500");
  });

  // toggle the share dropdown in communities
  $(".share-label").on("click", function(e) {
    e.stopPropagation();
    var isSelected = this.getAttribute("aria-selected") == "true";
    this.setAttribute("aria-selected", !isSelected);
    $(".share-label").not(this).attr("aria-selected", "false");
  });

  $(document).on("click", function() {
    $(".share-label").attr("aria-selected", "false");
  });

  // show form controls when the textarea receives focus
  $(".answer-body textarea").one("focus", function() {
    $(".answer-form-controls").show();
  });

  $(".comment-container textarea").one("focus", function() {
    $(".comment-form-controls").show();
  });


  //console.log("type of is " + typeof HelpCenter.user.organizations[0]);
  // Says typeof is string 
  
 if (HelpCenter.user.organizations[0] === undefined) {
    console.log("org is undefined");
    usrOrg = "none";
  }
  else {
    usrOrg = HelpCenter.user.organizations[0].name;
  }
  console.log("Help center user role is " + HelpCenter.user.role);
  if(HelpCenter.user.role === undefined) {
     console.log("user role is undefined");
    role = "none";
  }
  else {
    role = HelpCenter.user.role;
  }
  
  //Now pass the org and role to functions below
  hideFields(usrOrg, role);
  hideContent(usrOrg, role);
  getDL(usrOrg);

 ///////////////////////////////////////////////////////
////      Place the form description above the field

	$('.form-field>p').each(function(){
		$(this).insertAfter($(this).siblings('label'));
	});
	
 ///////////////////////////////////////////////////////
////  Add an HR element between each ticket field
$('.form-field>p').each(function(){
$(this).insertAfter($(this).siblings('label'));
});
$('.form-field').css("border-top","1px solid rgba(0, 0, 0, 0.15)");	
});


// Please do not delete below (JANRAIN customization)
function hideFields (usrOrg, role) {
   //alert("In hideFields");
  //Hide form fields for all but Acme Widget org users 
  console.log("hideFields role: " + role);
  console.log("hideFields org: " + usrOrg);
  if ((usrOrg !== "Acme Widget") && (role =="end_user")) {
    //this removes Acme Widget
    $(".request_custom_fields_24013513").remove();
    //this removes mobile field
   // $(".request_custom_fields_24003463").remove();
  }
  if ((usrOrg !== "Acme Inc") && (role =="end_user")) {
    //this removes Acme Inc field
    $(".request_custom_fields_24013593").remove();
  }
}


function hideContent(usrOrg, role) {
  console.log("user role: " + HelpCenter.user.role);
  console.log("hidecontent org: " + usrOrg);
   // if ((HelpCenter.user.role =="end_user") || (HelpCenter.user.role == "anonymous")) {
       if ((HelpCenter.user.role == "anonymous") || (usrOrg == "none")) {
      //Also remove the "my tickets and Activites links
       $(".my-activities").remove();
       $(".submit-a-request").remove();
       $("#li-request").remove();
       //Now widen and center the 3 remainer li's.
             $("#li-search").width(296);
      $("#li-issues").width(296);
      $("#li-request").width(296);
    }
    if ((HelpCenter.user.role == "anonymous") || (usrOrg == "none")) {
        //also redirect them to the community if a basic user figures out the path to submit a ticket.
        var l = location.pathname;
        console.log("Path is " + l);
        if(l == "/hc/en-us/requests/new") {
          window.location.replace("https://janrain1372039033.zendesk.com/hc/communities/public/topics");
        }
    }
}

window.addEventListener('load', hideContent, false);

function hideSubmit() {
    console.log("user role: " + HelpCenter.user.role);
    if (HelpCenter.user.role == "anonymous") {
      
      document.getElementById("show-community").style.visibility="visible";
      //Removehe li on the home page with the submit a request
      $("#li-request").remove();
      
      //Remove the link on the upper right hand
      $(".submit-a-request").remove();
      
      //Since we removed one li element, we need to widen the other 3 reamining li elements to center them.
      $("#li-search").width(296);
      $("#li-issues").width(296);
      $("#li-request").width(296);
      //This also works too, below:
      //$("#li-issues").css("width", 296);
      var l = location.pathname;
      console.log("Path is " + l);
      if(l == "/hc/en-us/requests/new") {
        window.location.replace("https://janrain1372039033.zendesk.com/hc/communities/public/topics");
      }
    }
    //If they're a paying customer, remove the community div
   // if((HelpCenter.user.role =="end_user") || (HelpCenter.user.role == "agent") || (HelpCenter.user.role == "manager")) {
     // $("#show-community").show();
    //}
}

window.addEventListener('load', hideSubmit, false);

function getDL(userOrg) {
  i=0;
  x=0;
  var l = location.pathname;
  //We need to get the DL list, and hide some dt's based on the    //user org for the requests/<ticket number> page
  // So, Get the path, and match up to requests/
  // The path may change depending on implementation
  
  if (/^\/hc\/en-us\/requests\//.test(l)) {

      ///////////////////////////////////////////////
     //   Add an ID to each DT, then hide it if it matches
    i=0;
  
    $('dt').each(function() {

      i = i +1;
      //console.log("i = " + i);
      $(this).attr('id', i);

      
      //console.log("closest dd: " + dx);
      
      //Now we remove the Acme Widget specific fields
      if ((usrOrg !== "Acme Widget") && (role =="end_user")) {
        
        //Now find the dt for the Acme Widget fild and hide it
        if($(this).text() == "Acme Widgete Only Ticket") {
          //console.log("Found match: " + $(this).text());
          //console.log("i is: " + i);
          //console.log()

          //remove the corresponding dd of the dt that has 
          // "Acme Widget Only ticket" first
          $("dt[id=" + i + "]").prevUntil( "dt" ).remove();
          // Now remove the DT that has the matching text
          // "Acme Widget Only Ticket"
          $("dt[id=" + i + "]").remove();
        }
      }
       ///////////////////////////////////////////////////////////////
      // Now if they're not Acme Inc, then remove Acme Inc field
      if ((usrOrg !== "Acme Inc") && (role =="end_user")) {
        
        //Now find the dt for the Acme Inc fild and hide it
        if($(this).text() == "Acme Inc Configuration Change Request") {
          console.log("Found match: " + $(this).text());
          //$("dt[id=" + i + "]").remove();
          console.log("i is: " + i);
          //console.log()

          //remove the corresponding dd of the dt that has 
          // "Acme Inc Configuration Change Request" first
          $("dt[id=" + i + "]").prevUntil( "dt" ).remove();
          // Now remove the DT that has the matching text
          // "Acme Inc Configuration Change Request"
          $("dt[id=" + i + "]").remove();
        }
      }
    
    })// End dt.each function ///////////////////
    
  }
}// end get DL

window.addEventListener('load', getDL, false);

// Get path
function addElement () {
  var a = location.pathname;
  //alert("Path is " + a);
  // Adds a class ot the home page that has an image background
  if(a == "/hc/en-us") {
    $("main").addClass("mainImage");
  }
  // Add an image behind the submit a new request 
  $( "main" ).wrapInner( "<div id='maincontainer'>" );

}
window.addEventListener('load', addElement, false);  

   ////////////////////////////////////////////////////
  //*** THIS WILL ELIMITEATE THE ESCAPED MARKUP ***///
$(document).ready(function() {

  var p = location.pathname;
      console.log("Path is " + p);
  if(p.match("requests") || p.match("questions")) {
    // target only <p> elements within divs to which the "form-field" class has been applied
    $('div.form-field p').html(function(e, orig) {

        // iteratively replace escaped characters (only < and > addressed here)
        return orig.replace(/&lt;/g, '<').replace(/&gt;/g, '>').replace(/&quot;/g, '');
    });
  }
///////////////////////////////
  //Now escape html in topic/forum descriptions
  if(p.match("topics")) {
    // target only <p> elements within divs to which the "form-field" class has been applied
    $('p.topic-description').html(function(e, orig) {

        // iteratively replace escaped characters (only < and > addressed here)
        return orig.replace(/&lt;/g, '<').replace(/&gt;/g, '>').replace(/&quot;/g, '');
    });
  }
});
  
  
  
  
