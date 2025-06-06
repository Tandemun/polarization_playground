---
layout: default
title: HWP-QWP Controller
---



<div id="controller"></div>
<div id="poincare"></div>  
<div style="display: flex; gap: 0px; flex-wrap: wrap; justify-content: center;">
    <div id="ellips0"></div>
    <div id="ellips1"></div>
    <div id="ellips2"></div>
</div>

 
<script>  
  var controller = new GGBApplet(createGGBParams("controller", "hqfm9sqy",), true);
  var poincare = new GGBApplet(createGGBParams("poincare", "rvbafww5",{enableRightClick: true}), true);
  var ellips0 = new GGBApplet(createGGBParams("ellips0", "ar9nzxm3"), true);
  var ellips1 = new GGBApplet(createGGBParams("ellips1", "ar9nzxm3"), true);
  var ellips2 = new GGBApplet(createGGBParams("ellips2", "ar9nzxm3"), true);

  window.onload = function () {
    controller.inject("controller")
    poincare.inject("poincare");
    ellips0.inject("ellips0");
    ellips1.inject("ellips1");
    ellips2.inject("ellips2");
  };

let appletsLoaded = {
  controller: false,
  poincare: false,
  ellips0: false,
  ellips1: false,
  ellips2: false
};


function setupAll() {	
    setMode(poincare, "threePoints");
    poincare.setValue("phi1", 90)
    poincare.setValue("phi2", 180)
    poincare.setColor("P0", 0,0,0)
    ellips0.setColor("ellips", 0, 0, 0)

    console.log("Set background colors for applets");
    const bgColor = getCssVariable("--base3")
    controller.setGraphicsOptions(-1,{"bgColor":bgColor});
    controller.setGraphicsOptions(1,{"bgColor":bgColor});
    poincare.setGraphicsOptions(-1,{"bgColor":bgColor});
    poincare.setGraphicsOptions(1,{"bgColor":bgColor});
    ellips0.setGraphicsOptions(1,{"bgColor":bgColor});
    ellips1.setGraphicsOptions(1,{"bgColor":bgColor});
    ellips2.setGraphicsOptions(1,{"bgColor":bgColor});
	
    setColors([
      { applet: controller, name: "paddle1" },
      { applet: controller, name: "th1" },
      { applet: poincare,   name: "P1" },
	    { applet: poincare,   name: "A11"},
	    { applet: poincare,   name: "A12"},
      { applet: poincare,   name: "P0P1"},
      { applet: ellips1,    name: "ellips"},  
    ], "--blue");

    setColors([
      { applet: controller, name: "paddle2" },
      { applet: controller, name: "th2" },
      { applet: poincare,   name: "P2" },
      { applet: poincare,   name: "A21"},
      { applet: poincare,   name: "A22"},
      { applet: poincare,   name: "P1P2"},
      { applet: ellips2,    name: "ellips"},  
    ], "--orange");    
	      
    syncValue(controller, "th1", poincare, "th1");
    syncValue(controller, "th2", poincare, "th2");  
    controller.registerObjectUpdateListener("th1", () => syncValue(controller, "th1", poincare, "th1"));
    controller.registerObjectUpdateListener("th2", () => syncValue(controller, "th2", poincare, "th2"));
    
    syncCoords(poincare, "P0", ellips0, "S");
    syncCoords(poincare, "P1", ellips1, "S");
    syncCoords(poincare, "P2", ellips2, "S"); 
    poincare.registerObjectUpdateListener("P0", () => syncCoords(poincare, "P0", ellips0, "S"));
    poincare.registerObjectUpdateListener("P1", () => syncCoords(poincare, "P1", ellips1, "S"));
    poincare.registerObjectUpdateListener("P2", () => syncCoords(poincare, "P2", ellips2, "S"));   
}
</script>


