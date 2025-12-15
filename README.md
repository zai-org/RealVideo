# RealVideo

RealVideo is a WebSocket-based video calling system that supports text input. It leverages **GLM-4.5-AirX** and 
**GLM-TTS** models to generate audio responses and utilizes autoregressive diffusion to generate corresponding 
video frames. The system features a modular design with full functionality and a clean code structure.
Visit [blog](https://z.ai/blog/realvideo) here!

## Example Video


<table border="0" style="width: 100%; text-align: left; margin-top: 20px;">
  <tr>
      <td>
          <video src="https://github.com/user-attachments/assets/4353a47f-32db-4f07-af68-c7cf4eb9b7ec" width="100%" controls autoplay loop></video>
      </td>
      <td>
          <video src="https://github.com/user-attachments/assets/13a674d7-9d2b-4979-be00-3ba37664252d" width="100%" controls autoplay loop></video>
      </td>
      <td>
          <video src="https://github.com/user-attachments/assets/e8e02325-5e63-4bfe-8ffc-c319cea5fe21" width="100%" controls autoplay loop></video>
      </td>
  </tr>
</table>

## Features

- **Text Input**: Supports text message input.
- **AI Voice Response**: Integrates GLM-4.5-AirX and GLM-TTS models to generate voice responses.
- **Lip Sync**: Generates real-time conversational video based on any input image and audio.
- **Real-time Communication**: WebSocket-based real-time bidirectional communication.

## Download

| Model                        | Download Links                                                                                                                                                       |
|------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    RealVideo          | [🤗 Hugging Face](https://huggingface.co/zai-org/RealVideo)<br>[🤖 ModelScope](https://modelscope.cn/models/ZhipuAI/RealVideo)                           |

## Quick Start

### 1. Requirements

- Python 3.10 - 3.12
- pip3
- Modern browser (supporting WebSocket and Web Audio API)

### 2. Install Dependencies

```bash
pip3 install -r requirements.txt
huggingface-cli download Wan-AI/Wan2.2-S2V-14B --local-dir-use-symlinks False --local-dir wan_models/Wan2.2-S2V-14B
```

### 3. Configure API Key

Before using, please set the ZAI API key:

```bash
export ZAI_API_KEY="your_actual_api_key_here"
```

and change `config/config.py` line:

```python
PATH_TO_YOUR_MODEL = "zai-org/RealVideo/model.pt"  # Replace with your model path
```

### 4. Start the Service

Specify the number of GPUs you wish to use and run the startup script, at least 2 GPUs (per 80GB, such as H100, H200).

For example:

```bash
CUDA_VISIBLE_DEVICES=0,1 bash ./scripts/run_app.sh
```

One GPU will be used for the VAE service, while the remaining GPUs will be automatically allocated for parallel
computation of the DiT service.

The table below shows reference times (in ms) for DiT to generate one block. If the time is within **500ms**, smooth
real-time generation can be achieved. Numbers in parentheses indicate the time taken with compilation enabled.

| DiT sp size / Denoising steps | 2                         | 4                     |
|-------------------------------|---------------------------|-----------------------|
| 1                             | 563.84 ms (**442.61 ms**) | 943.13 ms (723.06 ms) |
| 2                             | **384.86 ms**             | 655.92 ms (527.11 ms) |
| 4                             | **306.39 ms**             | 513.72 ms (**480.68 ms**) |

### 5. Access the Application

- **Main Page**: http://localhost:8003

## Usage Instructions

1. **Set Avatar and Voice**: Use the file upload button to upload an image to set the avatar, or upload a speech audio
   file longer than 3 seconds for voice cloning.
2. **Connect WebSocket**: Click the "Connect" button to establish the WebSocket connection.
3. **Text Input**: Enter a message in the text box and press Enter or click "Send" to send the message.
4. **Real-time Response**: The real-time generated video response will be displayed on the left.

## Technical Highlights

- **Model Integration**: Allows for convenient and quick voice cloning, taking text input to generate audio output.
- **Modular Design**: Clear code structure, easy to maintain and extend.
- **Real-time Performance**: Optimized audio processing and real-time video generation algorithms.

## Acknowledgements

This project utilizes the following open-source libraries:

- [self forcing](https://github.com/guandeh17/Self-Forcing)
- [Wan2.2-S2V](https://github.com/Wan-Video/Wan2.2)
