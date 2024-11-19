# ASCII Art Converter
🚧 Heads up! This project is still in development - expect breaking changes along the way. 🚧

![image](https://github.com/user-attachments/assets/9e4183e3-b970-4346-8563-5a87e825779c)

### Overview
Tool to generate ASCII art from images with edge and angle detection.

Written in pure Go using standard libraries and the `disintegration/gift` module.

### Pipeline

<details>
<summary>1. Original image </summary>
<img src="https://github.com/user-attachments/assets/c8af42ce-e296-4625-bf1c-ff6551ee5572" />
</details>

<details>
<summary>2. Preprocess the image with an <a href="https://users.cs.northwestern.edu/~sco590/winnemoeller-cag2012.pdf">Extended Difference of Gaussians filter</a> to accenuate boundaries</summary>
<img src="https://github.com/user-attachments/assets/a2cdcbe6-f434-467b-bebb-547b74deceda"/>
</details>

<details><summary>3. Detect edges from the XDoG Output via a <a href="https://en.wikipedia.org/wiki/Sobel_operator">Sobel filter</a> and calculate angles based on X/Y gradient magnitudes </summary>
  
  ```text
                                                                                                |       //             |      
                                                ____________                                   //      //              |      
                        _______         __________ ____    ______________                      \\    ///               |     /
                     ///      ___________                               ___________             \\__//                 |   ///
                 ////                                                              \______                             |  //  
              ////                                                                       ____\\                        |///   
           ///                                                 _________________              \\\\                            
       ////                                           _______/                   \___\_\|         ______                      
    ////                                         ______                                \\\             _\\                    
 __//                                       /____                                        \__              \\                  
                                          ///                                              \_\             \\___              
                                       _//                                                   /\_           \__  \\\           
 _\                                _///_                                                 /____/             \\_   \           
  \\\                          __/_                                                     /\_      \_/               \\         
    |                    _______                                                       /_//                          \\\      
    |                ////                                                           ////                               \|     
   /|              ///                                                          ___/_                                   |     
  //             |//                                                       /____        //|                             |     
 //             //                                                        |           /_  |\                            \\\   
               //                                    /__                  |          /     \\                             \|  
             ///                                ____/___                  |         |       \\                             |  
            //                            ____//____/                     |         _\       \\\\                         ||  
            /                      ________ _ ///                         |\         ||          ____                     /|  
 \\         \\               _____ |    //____          _____              \\\        |____        ___/                   |   
  \\          \\\            \__________/       ______________________       \\           ___________                     |   
   \\           \\\             _        /________                  __________/                                          //   
     \\           \\_____       /________/                                                                             //     
      \\\               ________/                                                                                    //       
        \\\                                                                                                         //        
          \\\                                                                                                     ///         
            \\\\                                                                                               ////           
                \___                                                                                       __///              
                    \\\\                                                                                ////                  
                        \\__                                                                         ////                     
                            _____                                                               ____/                         
                                 __________                                            _________                              
                                          _________                            _________                                      
                                                  ______________________________                                              
                                                                                                                              
                                                                                                                               
```
</details>


<details> <summary>4. Map the original image to ASCII characters based on luminence </summary>

```text
 ..............           .............                                           .......::::::***++%%%+*:::::::::::::***++++%
  ...............            .........        ...:::..::::::.........              .......::::****++%%+*:..:::::::::::***+++++
             ..        .:****::.........:::**+++++++++++++++++++++++++**:......      .......::****++%+*:....::::::::::***++++*
                   .:*++++++++++++++++++++++++++++++++++++++++++++++++**+++++++++**:.   ......:::*++*:.......:::...::::**+++*:
                .:*++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++*****+***::::....:::::...............:::*****:.
             .*++++++++++%%%%+++++++++++++++++++++++++++++++++++++++++++++++++++**+++++*+***++*:....................::****::..
         .:*++++++%%%%%+++++++++++++++++++++++++++++++++++++++++::*******:**+**+++++**++*******+*:::...............:::***::...
      .:*+++%%++++++++++++++++++++++++++++++++++++++++++*****:.  .:..........:...::***::*+**************:...........::::::....
   .:*+++++%%++%+++++++++++++++++++++++++++++++++++*::...:. . .....      .:..:::.:..:::**++++************+:.........::::......
 *++++++++%%++%%%+++++++++++++++++++++++++++++**: .. ...:      ..::     ...........::*:.::***+++**********+*:..  .............
 +++++++++%++++%%%+++++++++++++++++++++++++*:        .  ...... .::.   ..  ..*:......::::.:*::**++++*************:.............
 ++++++++%++%+%%%+++++++++++++++++++++++*:.    .     .:....... .:::...   ... .. ...:::.::.:::*****++*****+*******+*...........
 *++++++%++%%+%+++++++++++++++++++++**:...      ...:.       .... ....:.    ...::.:::::::***+*****+****+++%+*******+*...... ...
  .*+++%+%%%+%+++++++++++++++++++*:.::.:..       ...      ...........::... ....:.:::*:::******+*****++%%%+%+*******+*:.    ...
   .++%++%%+++++++++++++++***::......:::.. :              :............::..:::::::::*::::***+++%+:*+++++%%%%+*********+*: ....
   :+%++%%++%+++++++++*:......::..:.:*....                   .. ...::::*:::::::::::::**+++++++++++%++++++++%%***********+. ...
  .++++%%++%+++++++**.........:.. ...:*.. ...        :**.:.......::****:.::::.::**++++++******+%%%++++++++++%+*******+*++. ...
 .++++%%++++**++***:..:::.....:..   . .:.....        ..:..:::::::::::....:**+++++++*********+%%%%+++++++++++%******+++*++:....
 +++++++++%+**+****:.....:.:..............::.....   ...:***::::::.......::**%%+++++*+*******+%%%%%+++++++++++************++:..
 ++++++++++***+***::.:....::.::...........::::::..::*******:.:::..... ::::*+%%++++++****:****+%%%%%+++++++++***************+..
 +++++++++********:::::::.:....::...::::::.::************:::::..     :::::*+%%+++++****::::::*+%%%%%+++++++******+++++++**++..
 +++++++++*******::::..:::::..::::::::::**************::::.       ...:::::*+%%++++******:...:::**++%%%+++****++++++++****++:..
 *++++++++*******:::::::::.:::::******+**********::::.... ....    .:.....::*+%%+++++++*:::::::::::::*******++++++++******++..:
 *+++++++++*****:::::*:..:*********:*++******::. ..::::*******:...:::::::..::*+++++**********************+++++***********+%:::
  *+++++++++++***::::.::*::************::..:::::****************************:*****+++++***************+++++++************++.::
   :++++++++++++****::.::..:::::::::::::*******+**++*+++++*********************++++++++++++++++++++++++++++++++++******+++...:
     :*++++++++++++******:::::::***********+++++++++++**++++++***********++++++++++++++++++++++++++++++++++++++++***++++:....:
      .*+++++++++++++++++++******+++++++++***++++++++++++++++++++++++++++***++++++++++++++++++++++++**+++++++*******++:.......
        :*+++++++++++++++++++++***++++++++++***++++++++++++++++++++++++++++++++++++++++++++++++++++++++++**********++:........
          .*+++++++++++++++++++++**++++++++++***++++++++++++++++++++++++++++++++++++++++++++++++++++++***********++*..........
             :**++++*++++++++++++***+++++++++++***++++++++++++++++++++++++++++++++++++*++++++++++++**********++++:. ..........
                .:**++++++++++++++***++++++++++++***+++++++++++++++*++++++++++++++++++++****************++++**:.  ............
                     :**++++++++++****++++++++++++****+++++++++++++++****++++++++++++++++*************+++*..        ..........
                        .:**++++++******++++++++++++****+++++++++++++*********+++++++++++*********++++*:       .  ............
                            ..:**++++++++++++++++++*********+++++++++*****************+++++++++++*:..         ................
                                  ..::******+++++++++**********++++++++***********++++++**:::..           ....................
                                            ..:*****++++++++++++++****+++++++++++**::.                 .......................
                                                      .........    ........                            .......................
                                                                                                      ........................
                                                                                                   ...........................
```
</details>

<details><summary>5. Overlay the edges onto the base ASCII mapping </summary>

```text
 ..............           .............                                           .......::::::*|*++%%%+//::::::::::::*|*++++%
  ...............            .........        ..____________.........              .......::::*|/*++%%+//..:::::::::::*|*+++++
             ..        ._______.........__________+____++++______________......      .......::*\\*++%///....::::::::::*|*++++/
                   .:///++++++___________+++++++++++++++++++++++++++++**___________:.   ......::\\__//.......:::...::::|*++///
                .////++++++++++++++++++++++++++++++++++++++++++++++++++++++++++****\______::....:::::...............:::|**//:.
             .////+++++++%%%%+++++++++++++++++++++++++++++++++++++++++++++++++++**+++++*+____\\:....................::*|///:..
         .:///++++%%%%%++++++++++++++++++++++++++++++++++++++++_________________++++**++******\\\\::...............:::***::...
      .////+%%++++++++++++++++++++++++++++++++++++++++_______/.  .:..........:...\___\_\|+********______:...........::::::....
   .////+++%%++%+++++++++++++++++++++++++++++++++______..:. . .....      .:..:::.:..:::\\\+++**********_\\:.........::::......
 __//+++++%%++%%%+++++++++++++++++++++++++++/____ .. ...:      ..::     ...........::*:.:\__*+++**********\\:..  .............
 +++++++++%++++%%%++++++++++++++++++++++++///        .  ...... .::.   ..  ..*:......::::.:*\_\*++++********\\___:.............
 ++++++++%++%+%%%++++++++++++++++++++++_//.    .     .:....... .:::...   ... .. ...:::.::.:::/\_**++*****+*\__**\\\...........
 _\+++++%++%%+%++++++++++++++++++++_///_..      ...:.       .... ....:.    ...::.:::::::*/____/**+****+++%+*\\_***\*...... ...
  \\\++%+%%%+%+++++++++++++++++__/_.::.:..       ...      ...........::... ....:.:::*:::/\_***+**\_/++%%%+%+*******\\:.    ...
   .|+%++%%++++++++++++++_______.....:::.. :              :............::..:::::::::*::/_//*+++%+:*+++++%%%%+********\\\: ....
   :|%++%%++%++++++++////.....::..:.:*....                   .. ...::::*::::::::::::////++++++++++%++++++++%%**********\|. ...
  ./|++%%++%+++++++///........:.. ...:*.. ...        :**.:.......::****:.::::.::___/_+++******+%%%++++++++++%+*******+*+|. ...
 .//++%%++++**++*|//..:::.....:..   . .:.....        ..:..:::::::::::....:*/____+++*****//|*+%%%%+++++++++++%******+++*+|:....
 //+++++++%+**+*//*:.....:.:..............::.....   ...:***::::::.......::|*%%+++++*+*/_**|\+%%%%%+++++++++++***********\\\:..
 ++++++++++***+//*::.:....::.::...........::::::..::*/__***:.:::..... ::::|+%%++++++*/**:**\\+%%%%%+++++++++**************\|..
 +++++++++***///**:::::::.:....::...::::::.::***____/___*:::::..     :::::|+%%+++++*|**:::::\\+%%%%%+++++++******+++++++**+|..
 +++++++++**//***::::..:::::..::::::::::**____//____/*::::.       ...:::::|+%%++++**_\**:...:\\\\++%%%+++****++++++++****+||..
 *++++++++**/****:::::::::.:::::***________*_*///::::.... ....    .:.....:|\+%%++++++||::::::::::____******++++++++******+/|.:
 \\++++++++*\\**:::::*:..:***_____*|*++*//____:. ..::::*_____*:...:::::::..\\\+++++***|____********___/**+++++***********+|:::
  \\++++++++++\\\::::.::*::**\__________/..:::::______________________******:\\***+++++***___________*+++++++************+|.::
   \\+++++++++++\\\*::.::..:::::_:::::::*/________++*+++++**********__________/++++++++++++++++++++++++++++++++++******++//..:
     \\+++++++++++\\_____:::::::/________/*+++++++++++**++++++***********++++++++++++++++++++++++++++++++++++++++***+++//....:
      \\\+++++++++++++++________/+++++++++***++++++++++++++++++++++++++++***++++++++++++++++++++++++**+++++++*******+//.......
        \\\++++++++++++++++++++***++++++++++***++++++++++++++++++++++++++++++++++++++++++++++++++++++++++**********+//........
          \\\++++++++++++++++++++**++++++++++***++++++++++++++++++++++++++++++++++++++++++++++++++++++***********+///.........
            \\\\++++*++++++++++++***+++++++++++***++++++++++++++++++++++++++++++++++++*++++++++++++**********++//// ..........
                \___++++++++++++++***++++++++++++***+++++++++++++++*++++++++++++++++++++****************+++__///  ............
                    \\\\++++++++++****++++++++++++****+++++++++++++++****++++++++++++++++*************++////        ..........
                        \\__++++++******++++++++++++****+++++++++++++*********+++++++++++*********+++////      .  ............
                            _____++++++++++++++++++*********+++++++++*****************++++++++++____/         ................
                                 __________*+++++++++**********++++++++***********+++++_________          ....................
                                          _________*++++++++++++++****+++++++++_________               .......................
                                                  ______________________________                       .......................
                                                                                                      ........................
                                                                                                   ...........................
```
</details>

### Installation
To install as CLI:

```sh
go install github.com/jeffc25/asciiart@latest
```


To install as project dependency:
```sh
go get github.com/jeffc25/asciiart
```

### Usage
🚧 WIP 🚧
