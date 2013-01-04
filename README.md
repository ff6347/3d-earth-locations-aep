#After Effects 3D Locations Tutorial  
This tutorial will show you how to use VC Element and Locations.jsx to create a Globe in 3D space with a geo marker and text overlay.  

0 . Prerequisites
- [AE CS 4+](http://www.adobe.com/products/aftereffects.html)  
- [Videocopilot Element](https://www.videocopilot.net/products/element/)  
- [Sublime Text 2](http://www.sublimetext.com)  
- [Locations Script](http://aescripts.com/locations/)  
- [AEMap Script](http://aescripts.com/aemap/)  
- [Zorro Script](http://aescripts.com/zorro-the-layer-tagger/)  
- (optional) [Optical Flares](https://www.videocopilot.net/products/opticalflares/) / [Knoll Light Factory](http://www.redgiantsoftware.com/products/all/knoll-light-factory/) / or other 3D flare generator  

1 . Get the Data  
- [Natural Earth](http://www.shadedrelief.com/natural3/pages/textures.html) by Tom Patterson  
- NASA VIIRS [Earth At Night](http://earthobservatory.nasa.gov/NaturalHazards/view.php?id=79765)  
- [VideoCopilot 3D Earth](http://www.videocopilot.net/blog/2012/08/free-earth-project-for-element-3d/)  
- [Moon](http://www.celestiamotherlode.net/catalog/show_creator_details.php?creator_id=205) by Philip Iveic  
- [Sun](http://www.celestiamotherlode.net/catalog/sol.php) by Frank Gregorio  
- [US State Capitals Geocommos](http://geocommons.com/overlays/165342)  


##For The Nerds  

1. Create bigger normal Map  
2. Get Geo Data from geoTiff  

-----------------  

###Normal Maps  
Use [normal-map](https://github.com/sinisterchipmunk/normal-map) by sinisterchipmunk  
> Command line tool and Ruby library for generating normal maps.  
> Generates DOT3 bump maps, also known as normal maps, for use in 3D computing.  
by sinisterchipmunk
Works fine! Cool thing.  
[github Link](https://github.com/sinisterchipmunk/normal-map)  
MAC Requirements  
needs XCode and Command Line Tools installed, [rmagick](http://rmagick.rubyforge.org) which needs [ImageMagick](http://www.imagemagick.org/script/index.php):
    
    sudo port install ImageMagick  

than  

    sudo gem install rmagick  

 if the installation of ImageMagick fails it helped for me to fully uninstall zlib and jpeg using:    
    
    # clean out zlib  
    port clean --all zlib  
    sudo port clean --all zlib  
    sudo port install zlib  
    
    # clean out jpeg
    port clean --all jpeg  
    sudo port clean --all jpeg  
    sudo port install jpeg  


###Geo Data from geoTiff  

use this python script readgeoinfo.py  


    !/usr/bin/env python    
    from sys import argv    
    from osgeo import gdal    
    filetoread = argv    
    # print type(filetoread)    
    ds = gdal.Open(filetoread[1])    
    width = ds.RasterXSize    
    height = ds.RasterYSize    
    gt = ds.GetGeoTransform()    
    minx = gt[0]    
    miny = gt[3] + width * gt[4] + height * gt[5]    
    maxx = gt[0] + width * gt[1] + height * gt[2]    
    maxy = gt[3]
    
    if not gt is None:
        print 'Origin = (', gt[0] , ',', gt[3] ,')'
        print 'Pixel Size = (', gt[1] , ',', gt[5] , ')'
        print ''
        print 'min X = ',minx
        print 'min Y = ', miny
        print ''
        print 'max X = ' , maxx
        print 'max Y = ' , maxy

