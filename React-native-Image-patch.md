## The goal of this patch is to repair the react native problem of images not rendering in IOS

Install module patch package

    https://github.com/ds300/patch-package
    
Add the script 

    "script":{
        "postinstall": "patch-package"
    }
    
Open this file
        
    node_modules/react-native/Libraries/Image/RCTUIImageViewAnimated.m
    
Find this code
    
    - (void)displayLayer:(CALayer *)layer
    {
      if (_currentFrame) {
        layer.contentsScale = self.animatedImageScale;
        layer.contents = (__bridge id)_currentFrame.CGImage;
      }
      
Add the else statement to it.

    else {
        [super displayLayer:layer];
      }

run 
       
    npx patch-package react-native
This will create a folder called patch with a log of the patches

    
Run clean Build in xcode
Images should start appearing.
