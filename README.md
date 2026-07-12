# Qwen3.5-2B NPU
![Alt text](https://github.com/user-attachments/assets/6d297a34-c516-4cb1-be4a-bca471d40fa6)
<br><br>**User**:\<image\>Describe the image.<br><br>
**Answer**: This is a surreal, digitally manipulated image that blends science fiction with everyday life in an unexpected setting. Here’s a detailed description:

**Main Subject:**
- A person wearing a white astronaut suit reclines on what appears to be a lunar surface or spacecraft interior.
- Their legs are propped up against the edge of a green cooler box, which has faint graffiti-style writing (“SOMETHING”) visible on its side.
- In their right hand, they hold a bright green glass beer bottle — likely a craft beer — as if enjoying a drink in zero gravity.

**Setting & Background:**
- The environment is clearly extraterrestrial: gray, cratered terrain resembling the Moon’s surface.
- Behind the astronaut, Earth dominates the sky — its blue oceans and swirling white clouds are visible against the black void of space dotted with stars.
- To the right, part of a metallic ladder or structure leans into the frame, suggesting this might be inside a spacecraft or on a lunar module.

**Atmosphere & Style:**
- The lighting is dramatic — strong highlights on the astronaut’s helmet visor and suit, contrasting sharply with the dark background.
- There’s a sense of irony or absurdity: an astronaut relaxing with beer next to Earth, defying gravity and normal human behavior in space.
- The image has a hyper-realistic yet dreamlike quality, enhanced by digital effects like lens flares and atmospheric glow around Earth.

**Overall Impression:**
It’s a humorous, thought-provoking piece that plays on the contrast between isolation in space and comfort found in mundane pleasures — drinking beer while floating above our own planet. It invites reflection on human resilience, curiosity, and the strange ways we adapt to extreme environments.

------------

## Qwen3.5-2B VLM for RK3588 NPU (Rock 5, Orange Pi 5). <br/>
[![License](https://img.shields.io/badge/License-BSD%203--Clause-blue.svg)](https://opensource.org/licenses/BSD-3-Clause)<br/><br/>
Paper: [Qwen3 Technical Report](https://arxiv.org/pdf/2505.09388)<br/><br/>

------------

## Introduction

LLMs (Large Language Models) are neural networks trained on large text datasets to understand and generate language.<br>
VLMs (Vision-Language Models) add a visual encoder so the model can process images and text together.<br> 
A combined VLM+LLM system is often referred to as a multimodal model.

These models can be large—hundreds of millions to billions of parameters—which impacts accuracy, memory use, and runtime speed.<br>
On edge devices like the RK3588, available RAM and compute are limited, and even the NPU has strict constraints on supported operations.<br>
Because of this, models typically need to be quantised or simplified to fit.

Performance is usually expressed in tokens (words) per second.<br>
Once converted to RKNN, parts of the model can run on the NPU, improving speed.<br>
Despite these limits, models like Qwen3-2B run well on the RK3588 because the NPU efficiently accelerates the heavy math, and the vision encoder can be optimised. This makes advanced multimodal AI feasible on small, power-efficient devices.

------------

## Model performance benchmark (FPS)

All models, with C++ examples, can be found on the Q-engineering GitHub.<br><br>
All LLM models are quantized to **w8a8**, while the VLM vision encoders use **fp16**.<br>

| model         | RAM (GB)<sup>1</sup> | llm cold sec<sup>2</sup> | llm warm sec<sup>3</sup> | vlm cold sec<sup>2</sup> | vlm warm sec<sup>3</sup> | Resolution | Tokens/s |
| --------------| :--: | :-----: | :-----: | :--------: | :-----: | :--------:  | :--------: |
| [Qwen3.5-9B](https://github.com/Qengineering/Qwen3.5-9B-NPU) | 9.2 | 97.1 | 97.1 | 11.5  | 11.5 | 448 x 448 | 3.2 |
| [Qwen3.5-4B](https://github.com/Qengineering/Qwen3.5-4B-NPU) | 5.4 | 52.8 | 6.2 | 8.5  | 0.9 | 448 x 448 | 5.2 |
| [Qwen3.5-2B](https://github.com/Qengineering/Qwen3.5-2B-NPU) | 2.9 | 23.9 | 3.2 | 8.5  | 0.8 | 448 x 448 | 11.0 |
| [Qwen3.5-0.8B](https://github.com/Qengineering/Qwen3.5-0.8B-NPU) | 1.3 | 10.6 | 1.9 | 2.7  | 0.2 | 448 x 448 | 21.6 |
| [Qwen3-2B](https://github.com/Qengineering/Qwen3-VL-2B-NPU) | 3.1 | 21.9 | 2.6 | 10.0  | 0.9 | 448 x 448 | 11.5 |
| [Qwen3-4B](https://github.com/Qengineering/Qwen3-VL-4B-NPU) | 8.7 | 49.6 | 5.6 | 10.6  | 1.1 | 448 x 448 | 5.7 |
| [InternVL3.5-1B](https://github.com/Qengineering/InternVL3.5-1B-NPU) | 1.9 |  8.3 |   8.0 | 1.5    | 0.8 | 448 x 448 | 24 |
| [InternVL3.5-2B](https://github.com/Qengineering/InternVL3.5-2B-NPU) | 3.0 |  22 |   8.0 | 2.7    | 0.8 | 448 x 448 | 11.2 |
| [InternVL3.5-4B](https://github.com/Qengineering/InternVL3.5-4B-NPU) | 5.4 |  50 |   8.0 | 5.9    | 0.8 | 448 x 448 | 5 |
| [InternVL3.5-8B](https://github.com/Qengineering/InternVL3.5-8B-NPU) | 8.8 |  92 |   8.0 | 50.5    | 5.8 | 448 x 448 | 3.5 |
| [Qwen2.5-3B](https://github.com/Qengineering/Qwen2.5-VL-3B-NPU) | 4.8 | 48.3 |  4.0 | 17.9  | 1.8 | 392 x 392 | 7.0 |
| [Qwen2-7B](https://github.com/Qengineering/Qwen2-VL-7B-NPU) | 8.7 | 86.6 |   34.5 | 37.1  | 20.7 | 392 x 392 | 3.7 |
| [Qwen2-2.2B](https://github.com/Qengineering/Qwen2-VL-2B-NPU) | 3.3 | 29.1 |   2.5 | 17.1  | 1.7 | 392 x 392 | 12.5 |
| [InternVL3-1B](https://github.com/Qengineering/InternVL3-NPU) | 1.3 |  6.8 |   1.1 | 7.8    | 0.75 | 448 x 448 | 30 |
| [SmolVLM2-2.2B](https://github.com/Qengineering/SmolVLM2-2B-NPU) | 3.4 | 21.2 |   2.6 | 10.5   | 0.9  | 384 x 384 | 11 |
| [SmolVLM2-500M](https://github.com/Qengineering/SmolVLM2-500M-NPU) | 0.8 |  4.8 |   0.7 | 2.5    | 0.25 | 384 x 384 | 31 |
| [SmolVLM2-256M](https://github.com/Qengineering/SmolVLM2-256M-NPU) | 0.5 |  1.1 |   0.4 | 2.5    | 0.25 | 384 x 384 | 54 |

<sup>1</sup> The total used memory; LLM plus the VLM. <br>
<sup>2</sup> When an llm/vlm model is loaded for the first time from your disk to RAM or NPU, it is called a cold start.<br>
The duration depends on your OS, I/O transfer rate, and memory mapping.<br> 
<sup>3</sup> Subsequent loading (warm start) takes advantage of the already mapped data in RAM. Mostly, only a few pointers need to be restored.<br><br>
<img width="1000" height="700" alt="Plot_Tokens" src="https://github.com/user-attachments/assets/7342debe-769c-46c9-8a83-755caf7d67dc" /><br>
<img width="1000" height="700" alt="PlotMemory" src="https://github.com/user-attachments/assets/cf4362e6-f644-46d3-9b74-d129b23d3c44" />

------------

## Dependencies.
To run the application, you have to:
- OpenCV 64-bit installed.
- rkllm library.
- rknn library.
- Optional: Code::Blocks. (```$ sudo apt-get install codeblocks```)

### Installing the dependencies.
Start with the usual 
```
$ sudo apt-get update 
$ sudo apt-get upgrade
$ sudo apt-get install cmake wget curl
```
#### OpenCV
To install OpenCV on your SBC, follow the Raspberry Pi 4 [guide](https://qengineering.eu/install-opencv-on-raspberry-64-os.html).<br><br>
Or, when you have no intentions to program code:
```
$ sudo apt-get install libopencv-dev 
```
------------

## Installing the app.
```
$ git clone https://github.com/Qengineering/Qwen3-VL-2B-NPU
```

#### RKLLM, RKNN
To run InternVL3, you need to have the **rkllm-runtime** library version **1.3.0** installed, as well as the **rknpu driver** version **0.9.8**.<br>
If you don't have these on your machine, or if you have a lower version, you need to install them.<br>
We have provided the correct versions in the repo.<br>
```bash
$ cd ./Qwen3-VL-2B-NPU/aarch64/library
$ sudo cp ./*.so /usr/local/lib
$ cd ../include
$ sudo cp ./*.h /usr/local/include
```

Your rkllm model must match the library. If you use a model synthesized with the previous 1.2.3 rkllm library, and run it with the latest 1.3.0, you will get a malfunction. The internal Byte-Pair Encoding (BPE) dictionary parsing gets misaligned. 

### Download the LLM and VLM model.
The next step is downloading the models.<br>
Both can be downloaded from our Hugging Face page.<br>
- qwen3.5-2b-instruct_w8a8_rk3588.rkllm
- qwen3-vl-2b-vision_rk3588.rknn

Copy both into this folder.


## Building the app.
Once you have the two models, it is time to build your application.<br>
You can use **Code::Blocks**.
- Load the project file *.cbp in Code::Blocks.
- Select _Release_, not Debug.
- Compile and run with F9.
- You can alter command line arguments with _Project -> Set programs arguments..._ 

Or use **Cmake**.
```
$ mkdir build
$ cd build
$ cmake ..
$ make -j4
```

## Running the app

The application switches dynamically between Single Image Mode and Video Sequence Mode based on how many image files you pass into the arguments.

```bash
./VLM_VIDEO_NPU RKNN_model RKLLM_model file1.jpg [file2.jpg file3.jpg ...]
```


| Argument | Comment |
| --- | --- |
| RKNN_model | The visual encoder model (VLM) compiled for the NPU. |
| RKLLM_model | The large language model (LLM) compiled for the NPU. |
| file1.jpg ... | The images you want to process.<br>Passing 1 file triggers **Image Mode**.<br>Passing multiple files triggers **Video Sequence Mode**. |

In the context of the Rockchip RK3588 LLM (Large Language Model) library, `NewTokens` and `ContextLength` control the boundaries for text generation and memory allocation.<br><br>
In `main.cpp` you will find the line:<br>  
```cpp
RKLLM.LoadModel(vlm_model, llm_model, NewTokens, ContextLength);
```
Here you set you context based on available memory.<br><br>
**NewTokens**
This sets the maximum number of tokens (pieces of text, typically sub-word units) that the model is allowed to generate in response to a prompt during a single inference round. For example, if set to 300, the model will not return more than 300 tokens as output, regardless of the prompt length. It is important for controlling generation length to avoid run-on responses and manage resource use.<br><br>
**ContextLength (Dynamic KV Cache)**
This specifies the maximum total number of tokens the model can hold in its memory at once, which includes the system prompt, the massive image/video embeddings, your text questions, and all previous generated answers.
We have synthesized the models with a larger KV Cache than normally. Ours can hold up to 16384 tokens!
* **For 32GB Boards (e.g., Rock 5C 32GB):** You can safely push the KV Cache to `8192` or `16384` to support processing long video sequences and maintaining deep, multi-turn conversations without the model forgetting the image.
`RKLLM.LoadModel(vlm_model, llm_model, 2048, 16384);`

* **For 8GB/16GB Boards:** The KV cache is highly memory-intensive. You should keep this at `2048` or `4096`. If you set this higher than your physical RAM can handle, the Linux Out-Of-Memory (OOM) killer will crash the application.
`RKLLM.LoadModel(vlm_model, llm_model, 2048, 4096);`


**Typical Command Line Examples:**

Single Image Mode:

```bash
./VLM_VIDEO_NPU ./models/qwen3-vl-2b-vision.rknn ./models/qwen3-vl-2b-instruct.rkllm ./frame1.jpg 

```

Video Sequence Mode (Passing multiple frames):

```bash
./VLM_VIDEO_NPU ./models/qwen3-vl-2b-vision.rknn ./models/qwen3-vl-2b-instruct.rkllm ./frame1.jpg ./frame2.jpg ./frame3.jpg

```

## Using the app

Using the application is simple. Once you provide the model and the media files, you can ask anything you want.<br>
Remember, we are on a bare Rock 5C, so don't expect the same speed or quality as massive server-grade models like ChatGPT. On the other hand, as you will see in the examples below, the app performs amazingly well on the edge!

**Interacting with Media:**

* If you passed a **single image** and want to talk about it, you must include the `<image>` tag in your prompt. (e.g., `"Describe this <image> in detail."`)
* If you passed **multiple images (video sequence)**, you must use the `<video>` tag instead. (e.g., `"What action is happening in this <video>?"`)

**Chat Controls:**

* The app remembers the dialogue context continuously. To wipe the model's memory and start a fresh conversation about the loaded media, type `clear`.
* To leave the application, type `exit`.

## C++ code.  
Below, you find the surprisingly little code of main.cpp. 
```cpp
#include "RK35llm.h"
#include <vector>

int main(int argc, char** argv)
{
    // Usage: ./VLM_VIDEO_NPU vlm_model llm_model frame1.jpg [frame2.jpg frame3.jpg ...]
    if (argc < 4) {
        std::cerr << "Usage: " << argv[0] << " vlm_model llm_model file1.jpg [file2.jpg file3.jpg ...]\n"; 
        return -1;
    }

    std::string vlm_model = argv[1];
    std::string llm_model = argv[2];

    RK35llm RKLLM;
    RKLLM.SetInfo(true);
    RKLLM.SetSilence(false);

    RKLLM.LoadModel(vlm_model, llm_model, 2048, 16384);

    // Collect all image frames from arguments
    std::vector<cv::Mat> frames;
    for (int i = 3; i < argc; ++i) {
        cv::Mat frame = cv::imread(argv[i]);
        if (!frame.empty()) {
            frames.push_back(frame);
        } else {
            std::cerr << "Warning: Could not load image file: " << argv[i] << "\n";
        }
    }

    if (frames.empty()) {
        std::cerr << "Error: No valid images loaded. Exiting.\n";
        return -1;
    }

    // Dynamic routing: single image vs. video sequence
    if (frames.size() == 1) {
        std::cout << "\n[Info] Loading single image mode...\n";
        RKLLM.LoadImage(frames[0]);
    } else {
        std::cout << "\n[Info] Loading video sequence mode (" << frames.size() << " frames)...\n";
        RKLLM.LoadVideoFrames(frames);
    }

    std::string input_str;
    std::string output_str;

    while (true) {
        printf("\nUser: ");
        std::getline(std::cin, input_str);
        if (input_str == "exit") break;

        // Reminder: the user must input the correct tag (<image> or <video>) based on the mode!
        output_str = RKLLM.Ask(input_str);
    }

    return 0;
}
```
Most code speaks for itself. One remark.<br>
The LLM generates the answer to your request in little pieces of text. You see them as if the LLM is typing on your terminal.<br>
RKLLM.SetSilence controls this behaviour. When set to `true`, it will suppress this output. RKLLM.Ask() also returns the complete answer.<br>
In main.cpp uncomment this line:
```cpp
std::cout << "\nLLM Answer: " << output_str << std::endl;
```

------------

## VLM examples.
| Image         | Dialog |
| --------------| --  |
| ![Singapore_S](https://github.com/user-attachments/assets/e742059a-3bdb-41be-9647-e7767da12ce6) |**User**: \<image\>Which city is this?<br>**Answer**: This is **Singapore**.<br>The image shows a famous view of Singapore’s skyline at dusk or dawn, featuring:<br>- The **Marina Bay Sands** hotel (with its distinctive three-tower structure and sky park) on the left.<br>- The **Singapore Flyer**, one of the world’s largest observation wheels, to the right.<br>- A calm body of water in the foreground reflecting the city lights — likely Marina Bay or Gardens by the Bay.<br>These landmarks are iconic symbols of Singapore, a city-state known for its modern architecture, blend of heritage and innovation, and vibrant urban life. The long exposure effect on the water gives it a smooth, dreamy quality often seen in travel photography.<br>✅ So, this is definitely **Singapore**. | 
| ![ChineseWall_S](https://github.com/user-attachments/assets/3ba4b57a-4b22-4050-b995-9599c6d239de) |**User**: \<image\>Tell me something about the history of this place.<br>**Answer**: The image you’ve shared depicts a section of the **Great Wall of China**, specifically in what appears to be the **Northwestern Frontier region** — likely near **Tianjin, Hebei Province**, or possibly further north toward **Shandong**. This area is historically significant for several reasons:<br>🏛️ Historical Context & Significance<br>1. **Strategic Importance of the Northern Border**<br>The Great Wall was built primarily to protect China from invasions by nomadic tribes such as the **Xiongnu**, **Yuan**, and later the **Mongols**. The northern frontier faced constant threats, so fortifications like this one were essential for defense.<br>2. **Location: Tianjin/Hebei Border**<br>This particular stretch of wall is located along the border between modern-day **Tianjin (China)** and **Manchuria (Russia)**. It was part of the ancient **Liaodong Peninsula campaign**, where Chinese forces attempted to hold off Russian expansion into Manchuria during the late Qing Dynasty.<br>In 1860, after the Opium Wars, Russia had already begun encroaching on Chinese territory in Manchuria. The Great Wall here served as a symbolic and practical barrier against further invasion — though it was never fully completed or maintained due to resource constraints and shifting geopolitical priorities.<br>3. **Architectural Style & Construction**<br>The wall shown is built of **brick and stone**, with watchtowers, gatehouses, and ramparts typical of Ming Dynasty construction. The use of local materials (clay bricks) reflects adaptation to the region’s geography. Some sections show signs of later modifications or repairs, indicating its long service over centuries.<br>4. **Cultural & Symbolic Role**<br>Beyond military function, the Great Wall became a powerful symbol of Chinese sovereignty and resilience. It was also used as a border marker between China and Russia for much of the 20th century — even after formal treaties ended direct territorial disputes in Manchuria by the early 1950s.<br>📜 Key Historical Events Nearby<br>- **Late Qing Dynasty (1860–1890s)**: The wall was used to resist Russian advances into Northeast China.<br>- **Sino-Soviet Border Disputes**: During the Cold War, both sides claimed parts of this border region, leading to tension and occasional skirmishes along the Great Wall.<br>- **Modern Era**: Today, much of the original structure has been preserved as a tourist attraction or historical site, though some sections have been restored for public access.<br>🌿 Natural Setting & Preservation<br>The lush green hillsides surrounding the wall suggest this area was once part of fertile agricultural land — ideal for sustaining large populations and supporting military operations. Today, conservation efforts focus on preserving these historic structures while allowing visitors to experience their grandeur safely.<br>💡 Fun Fact<br>There’s a famous legend that says the Great Wall was built by **Emperor Gaozu of Han** (202 BC) — though historians debate whether this is fact or folklore. Regardless, the wall’s enduring presence testifies to its strategic value and cultural importance.<br>If you’re visiting this location today, it’s a great place to see how history meets nature — standing as a silent guardian of centuries past against the backdrop of rolling mountains and clear skies. Let me know if you’d like more details about specific eras or nearby sites!|
| ![Pizza_S](https://github.com/user-attachments/assets/26fd5da3-f491-4b48-978a-14eae0819247) |**User**: \<image\>What are the ingredients I need to make this?<br>**Answer**: To make a pizza like the one in the image — which appears to be a classic **Margherita pizza** with a rustic, charred crust and fresh basil — you’ll need these core ingredients:<br>🍕 Core Ingredients:<br>1. **Pizza Dough (or pre-made dough)**<br>   - Flour (all-purpose or bread flour)<br>- Water<br>- Salt<br>- Optional: yeast (for leavened dough), or store-bought pizza dough<br>> *Tip: For authentic Neapolitan-style crust, use a simple 2:1 ratio of flour to water and let it rise naturally.*<br>2. **Tomato Sauce**<br>- San Marzano tomatoes (preferably canned in their own juice)<br>- Garlic (optional but common)<br>- Olive oil<br>- Salt & pepper<br>> *Note: You can also make your own sauce from fresh tomatoes, or use a pre-made marinara.*<br>3. **Mozzarella Cheese**<br>- Fresh mozzarella (preferably buffalo mozzarella for stretchiness)<br>- Or part-skim mozzarella if fresh isn’t available<br>>*Tip: Mozzarella should be sliced into rounds and placed on top before baking — it melts beautifully.*<br>4. **Fresh Basil Leaves**<br>- Fresh basil leaves (optional, but essential for this style)<br>>*Place them gently over the cheese after baking to preserve their color and aroma.*<br>Optional Additions:<br>- **Olive oil** – drizzled on top before baking or brushed onto dough<br>- **Garlic** – minced garlic added to sauce or dough<br>- **Extra virgin olive oil** – for brushing the crust during baking (especially important for that charred look)<br>Optional Toppings:<br>- Ham, salami, pepperoni → *not in this image*<br>- Mushrooms, onions, peppers → *also not present*<br>✅ So, to summarize — **you need:**<br>Flour, water, salt, tomato sauce, mozzarella cheese, fresh basil leaves, and optionally garlic or olive oil.<br>This combination creates the simple yet delicious Margherita-style pizza shown in your image! 🍅🧀🌿<br><br>**User**:What is the first step?<br>**Answer**:The **first step** to making this pizza — especially if you’re starting from scratch with dough — is:<br>✅ **1. Make or Prepare the Pizza Dough**<br>Start by mixing your flour, water, and salt (and optionally yeast or baking powder) in a bowl. Knead until smooth, then let it rest for 30–60 minutes to relax the gluten before shaping.<br>> 💡 *Pro tip: For authentic Neapolitan-style crust, use minimal kneading — just enough to form a ball — and let it rise naturally at room temperature.*<br>🔄 Then proceed with:<br>- Shaping the dough into a round (or oval)<br>- Preheating your oven (especially if using wood-fired or stone oven)<br>- Adding sauce, cheese, basil<br>- Baking until crust is golden and charred<br>But since you asked for the **very first step**, it’s always:<br>> 🥣 **Mix and knead the dough.**<br>Let me know if you want a recipe or tips for any part!|
| ![Titanic_S](https://github.com/user-attachments/assets/bf6da76c-c9a4-41c6-bea1-2b4411dd4013) |**User**: \<image\>Which movie is this?<br>**Answer**: This image is from the 2017 film **Titanic**, directed by James Cameron.<br>The scene features Leonardo DiCaprio as Jack Dawson and Kate Winslet as Rose DeWitt Bukater standing on the bow of the ship *Titanic* during a dramatic sunset or sunrise. Their poses — arms outstretched, embracing tightly — capture the emotional climax of their romance aboard the sinking vessel. The warm lighting and ocean backdrop are iconic to this pivotal moment in the movie’s narrative.<br>While it could be mistaken for other romantic dramas like *The Notebook*, the specific costumes (19th-century style), the ship’s rigging, and the cinematic composition strongly point to Cameron’s adaptation of Stephenie Meyer’s novel.<br>✅ **Movie**: *Titanic* (2017)  <br>🎬 Director: James Cameron <br>💥 Iconic scene: Jack and Rose on the bow at sunset|

## Video example.
## LLM example.
Notice the nice Markdown makeup of the answer!<br><br>
**User**: Can you make me a C++ call that embeds the Pythagorean theorem?<br><br>
**Answer**: Certainly! Here’s a clean, modern C++ function that computes the length of the hypotenuse using the Pythagorean theorem: `a² + b² = c²`, so `c = √(a² + b²)`.

```cpp
#include <iostream>
#include <cmath>  // for std::sqrt

// Function to compute the hypotenuse given two legs of a right triangle
double getHypotenuse(double a, double b) {
    return std::sqrt(a * a + b * b);
}

int main() {
    double leg1 = 3.0;
    double leg2 = 4.0;

    double hypotenuse = getHypotenuse(leg1, leg2);

    std::cout << "Legs: " << leg1 << ", " << leg2 << std::endl;
    std::cout << "Hypotenuse: " << hypotenuse << std::endl;

    return 0;
}
```

### How it works:
- We use `std::sqrt()` to compute the square root of the sum of squares.
- The function is modular and reusable — you can pass any two positive numbers as legs, and it will return the hypotenuse.
- In `main()`, we test with classic 3-4-5 triangle values for clarity.

### Example Output:
```
Legs: 3, 4
Hypotenuse: 5
```

Let me know if you’d like to extend this — e.g., add input validation, handle floating-point precision issues, or visualize the result!

------------

## **[Rock5GPT](https://rock5gpt.qengineering.eu)**
To get a taste, try our professional Qwen3 AI-chatbot running on a Rock 5C: https://rock5gpt.qengineering.eu
<img width="815" height="1151" alt="Rock5GPT" src="https://github.com/user-attachments/assets/3ce5ad31-bc2b-4513-8ac9-42be793a86db" /><br>

------------

[![paypal](https://qengineering.eu/images/TipJarSmall4.png)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=CPZTM5BB3FCYL) 




