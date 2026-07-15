# Optical Character Recognition with RPi
The microphone captures voice commands, and the Raspberry Pi processes them using softwares to trigger actions like text scanning. After recognizing the text, the device reads it out loud through the speaker. This tool serves both accessibility and educational purposes, by assisting the visually impaired through reading the text out loud and supporting language learners with pronunciation and listening.


| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Serena Z | No.2 High School of East China Normal University | Electrical Engineering | Incoming 10th grade

**Replace the BlueStamp logo below with an image of yourself and your completed project. Follow the guide [here](https://tomcam.github.io/least-github-pages/adding-images-github-pages-site.html) if you need help.**

![Headstone Image](logo.svg)
  
# Final Milestone

<iframe width="560" height="315" src="https://www.youtube.com/embed/mqI8-Abo-D4?si=EKvofUFefMj5y0Ey" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

I’ve implemented multilingual support. Technically, the system works like this: Tesseract OCR extracts text from images in four languages, including English, Chinese, French, and Spanish, with language packs installed to enable multilingual support. For speech output, I added Edge TTS engine. While eSpeak runs offline and handles English, French, and Spanish well, but it cannot read Chinese properly. Edge TTS solves this — when online mode is enabled and Chinese text is detected, the system automatically switches to Edge TTS for natural Chinese pronunciation. The user can switch between online and offline modes anytime using voice commands or keyboard, and the system deals with internet failures by falling back to eSpeak.

My biggest challenge was actually the SSH connection, I ran into a lot of issues there, and since I’ve already explained that part in detail below in the First Milestone section, I won’t repeat it all here. Another major challenge I faced was when I added aggressive preprocessing filters to remove background noise from the breadboard. These filters went too far and started removing fine details needed for Chinese character detection, so the system suddenly stopped recognizing Chinese altogether. I went back to the last working version, gradually re-added the filters with weaker settings, and found a balance between removing noise and remaining text clarity. 

Throughout this project, I gained experience in several key topics. First, hardware-software integration. I learned how to connect and configure components like the camera, microphone, and speaker on a Raspberry Pi. Second, offline AI models. I worked with Vosk for speech recognition and Tesseract for OCR, both running locally on the device. Third, image preprocessing. I understood how techniques like resizing, grayscale conversion, and thresholding directly impact OCR accuracy. Fourth, the ability of debugging and problem-solving, from fixing audio sample rate issues to troubleshooting SSH connections and environment management.

Looking ahead, I want to continue exploring AI-related projects with the Raspberry Pi, particularly in the area of human-computer interaction. I'm also interested in trying out Arduino for robotics and sensor-based projects, since it offers a different approach to hardware control.


# Second Milestone

<iframe width="560" height="315" src="https://www.youtube.com/embed/P-nca7DA0sM?si=mtzGq3tXl9UR2Skp" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

The base system relies on three core technologies. First, the microphone uses Vosk, which is an offline speech recognition engine that listens through the microphone and converts my voice commands into text. Second, after the camera takes a photo, the image goes through preprocessing steps like resizing, grayscale conversion, and thresholding to make the text clearer, and then Tesseract OCR extracts the actual text from the image. Third, the speaker relies on eSpeak, an offline speech synthesizer that reads the extracted text aloud through the speaker. When I switch to online mode, it uses Edge TTS for more natural Chinese pronunciation. These three components — Vosk, Tesseract, and eSpeak — work together as a complete offline-compatible pipeline. One surprising discovery was that even with a low-resolution camera, the preprocessing steps still made text extraction possible. Another challenge was integration — every time I added a new component, the system would break, even though each part worked perfectly on its own. I had to revise the code multiple times to get everything working together. A few lessons learned: always check the microphone's sample rate and make sure the speaker volume is properly set. Looking ahead, I hope my system will eventually support multiple languages, such as Chinese, French, and Spanish.

# First Milestone


<iframe width="560" height="315" src="https://www.youtube.com/embed/UEq7qhS2AMM?si=RUkRT2JAVURhNseN" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>  


This optical recognition project uses a Raspberry Pi as the core hardware with a camera and microphone for input and a speaker as an output; I connect my Mac to the Pi via SSH by entering its username and hostname in the Mac terminal, and enable VNC over SSH to open the Pi’s graphical desktop remotely on my Mac, where I can edit code and run project scripts without physical monitors or peripherals attached to the Pi. I have faced two main challenges: frequent SSH connection failures that required repeated SD card reflashes, and poor camera text recognition caused by low-quality captured images. To improve stability long-term, I will learn to troubleshoot broken SSH configurations and network settings directly within the Pi’s operating system instead of fully resetting the device and adjust lighting plus add image preprocessing to sharpen photos for better OCR accuracy. My plan is to finish all core base code in the second week, then spend the final week making only software modifications with no changes to my Raspberry Pi, camera or microphone hardware setup.

# Schematics 
Here's where you'll put images of your schematics. [Tinkercad](https://www.tinkercad.com/blog/official-guide-to-tinkercad-circuits) and [Fritzing](https://fritzing.org/learning/) are both great resoruces to create professional schematic diagrams, though BSE recommends Tinkercad becuase it can be done easily and for free in the browser. 

# Code
Here's where you'll put your code. The syntax below places it into a block of code. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize it to your project needs. 

```c++
void setup() {
  // put your setup code here, to run once:
  Serial.begin(9600);
  Serial.println("Hello World!");
}

void loop() {
  // put your main code here, to run repeatedly:

}
```

# Bill of Materials


| **Part** | **Note** | **Price** | **Link** |
|:--:|:--:|:--:|:--:|
| Raspberry Pi Kit | Used for processing data and controlling everything | $96.79 | <a href="https://www.amazon.com/RasTech-Raspberry-Starter-Heatsink-Screwdriver/dp/B0C8LV6VNZ/ref=sr_1_4?crid=3506HY00MCGVM&dib=eyJ2IjoiMSJ9._zkM62vSQ8p7tNr88715LdMv_qHh72Je-tkF9PXEa3chDE53QT4aZu4AGAb4ihE61QY4ZD55nKF6Fp2Kfs8t7AbafM_JrlJFfHo9OB4eAVGqa0EB-7aoBQHPmhKHZ2MW8ny-Kd44bMVlVxPlTWVk5YHIN5P3uKVqrE5Dcal0rKkHny-O6Xyb5ux2AOU6OwVbkag_bqBX66RQNRrgBuz-0pS43mcx93IZTQA9R8NaJJypYU2HAycp-XicTFmyU60a01Nfm9iuyo6B9yA8ppN3OQQyJ-NQ9xyNPxfTLwkqtng.yAYpU6outhQcZmOZhN9Wb6yTw7A85CNUbXZguGInZNg&dib_tag=se&keywords=raspberry%2Bpi%2Bkit&qid=1718848547&s=electronics&sprefix=rasbperry%2Bpi%2Bkit%2Celectronics%2C83&sr=1-4&th=1"> Link </a> |
| Picam w stand	| Used for taking pictures of the text | $10.99 | <a href="https://www.amazon.com/Arducam-Raspberry-Camera-Module-1080P/dp/B07RWCGX5K/ref=sr_1_10?crid=1U9IECPRDX3WW&dib=eyJ2IjoiMSJ9.EQptXsj1i39Y9oggTYxdai89FVefBqmO-xGB4sBBTHO4SEXcCZUKpLs1pTfSI2UV6zy9s3AQs7Evflr1mgvYz1YCSz3mqc1fKoWJuY2h_sLEdwqeJmnuUHIk2vmkOBLRlXijApDdRtOGjvFpd22kZibWh01QrWXaEwqpEp-2yRu8AwtKM3-xvdpkUNxIUIbjqrSK_cZ26yCkFh88Ih6aKDnMHVzWvkGv8cZGmAsc7eT7RKndhuCD03QQCco8ZhufAfPk0RJ-nafMKigKik2-9dEEZYTcX1D5vsv4x-weTH8.wWxtDi-AjBJ6-FuY_isVSX857HXALzCvS0vuocOJ6xg&dib_tag=se&keywords=arducam%2Bpicam&qid=1747573778&s=electronics&sprefix=arducam%2Bpicam%2Celectronics%2C89&sr=1-10&th=1"> Link </a> |
| Speaker | Used for reading the text out loud | $13.99 | <a href="https://www.amazon.com/Mobile-Speaker-Compact-Adhesive-Installation/dp/B0D95ZYCW6/ref=sr_1_21?crid=369CH18NKBSVU&dib=eyJ2IjoiMSJ9.fGxmsmnwIDfWJ86jFkBj2M9zmcDcTJDJ5mrEoKbPoNrsWxuJa_dYL6qoeEOWDCdistvn0ql7KvLvdE5jqDr0-IY9Hn9YsWu1Oy3eXWFB1iXZCoK66NzPfzialhjLhJGKAL7YU3iBTpfb7gJ5oM3pnHuzh9tfRA-QkKQPcTNZS39EEGN-fitqnkFQOGbfjIMaJcyEuFZuUIz8bj94BBA1-cHcB6OZ-uoxfiZAST_tFX8.8v-xvor8mw64ExKDR3N29OV45k1u_23oDE4b4od7GiM&dib_tag=se&keywords=speakerphone%2Bsmall%2Baudio%2Bjack&qid=1747574092&sprefix=speakerphone%2Bsmall%2Baudio%2Bjack%2B%2Caps%2C85&sr=8-21&th=1"> Link </a> |
| Microphone | Used for receiving the voice command | $9.99 | <a href="https://www.amazon.com/DUNGZDUZ-Microphone-Computer-Sensitivity-Mini-Sized/dp/B0CNVZ27YH/ref=sr_1_7?crid=2E8AID5UQ1ZZZ&dib=eyJ2IjoiMSJ9.ALlacqVSJFYCMwk0BLBt4BE78M6dbL4aQxGWFHFGViY7QOzmOSfkxRzzMD4BytGFdvrXnYFwbFQpiWeLB37vgMOeTgeyNJDCEdkcPjHzzHRJxfNFVUN6RfiMHaRcFDG-9Bv_yfPh1GhToIG1whgMGesfk7lXYtf8SFgQiEq2amOZxI0tqGpX2VQclkxKSnqhF6yzTiCWcZ4eNLkG1Dd01JochzymYWm59TYI_ipygVEt9UpdCReF2L_Ap0gIyhTLupQRKLocdolLZufM8LKLonKajGSQwrgEu_3jmlV10mM.wRiTmzhi2KBZXCOWVMCU_b0r9fvSClHWCv29BKgVQ4o&dib_tag=se&keywords=usb+microphone&qid=1747574148&sprefix=usb+microphone+%2Caps%2C143&sr=8-7"> Link </a> |

# Other Resources/Examples
One of the best parts about Github is that you can view how other people set up their own work. Here are some past BSE portfolios that are awesome examples. You can view how they set up their portfolio, and you can view their index.md files to understand how they implemented different portfolio components.
- [Example 1](https://trashytuber.github.io/YimingJiaBlueStamp/)
- [Example 2](https://sviatil0.github.io/Sviatoslav_BSE/)
- [Example 3](https://arneshkumar.github.io/arneshbluestamp/)

To watch the BSE tutorial on how to create a portfolio, click here.
