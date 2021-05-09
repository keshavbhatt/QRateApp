# QRateApp
Intelligent App Rating dialog for Qt applications


## Features

 1. Fully Customizable 
 2. Set the show delay based on number of times the user opened your application 
 3. Set the show delay based on number of days user has installed your app on his system
 4. Set  the show delay in milliseconds after which the app rate dialog should open if all show dialog conditions are satisfied
 5. Shows dialog only when user is interacting with the application (application is not minimized or user has no focus)
 6. Other intelligence baked in which will not irritate users and ask them gracefully rate your application 

## Requirements
You need Qt 5 or above

## How to use in your Qt Project
Go to your project's source directory, clone the repository to `RateApp` directory. (You can remove unwanted files likes images etc once done)

    git clone https://github.com/keshavbhatt/QRateApp.git RateApp 

 Add the .pri file in your project's .pro file like below.

     include(RateApp/RateApp.pri)
In your code initialize the Widget like this:
For more APIs, customizations, go through source code.

    RateApp  *rateApp  =  new  RateApp(this,  "URL_TO_OPEN_WHEN_USER_CLICK_RATE_BUTTON",  APP_LAUNCH_COUNT,  APP_INSTALLED_DAYS,  DELAY_IN_MIILISECONDS);
    
      rateApp->setWindowTitle(QApplication::applicationName()+"  |  "+tr("Rate  Application"));
    
      rateApp->setVisible(false);
    
      rateApp->setWindowFlags(Qt::Dialog);
    
      rateApp->setAttribute(Qt::WA_DeleteOnClose,true);
    
      QPoint  centerPos  =  this->geometry().center()-rateApp->geometry().center();
    
      connect(rateApp,&RateApp::showRateDialog,[=]()
    
      {
    
      if(this->windowState()  !=  Qt::WindowMinimized  &&  this->isVisible()  &&  isActiveWindow()){
    
      rateApp->move(centerPos);
    
      rateApp->show();
    
      }else{
    
      rateApp->delayShowEvent();
    
      }
    
      });

## Screenshots
![Screenshot showing the widget being use in one of my application WhatSie](https://github.com/keshavbhatt/QRateApp/blob/main/images/1.png?raw=true)
Screenshot showing the widget being use in one of my application [WhatSie](https://snapcraft.io/whatsie) (WhatSie is a full fledged WhatsApp Web client for Linux Desktop)

