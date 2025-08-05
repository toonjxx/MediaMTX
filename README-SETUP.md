# MediaMTX Setup for ThanhPhong Auto

This directory contains the Docker configuration for running MediaMTX, a versatile media server that converts RTSP streams from your Hikvision cameras to various formats including HLS and WebRTC for web viewing.

## Quick Start

1. Make sure Docker is installed on your system
2. Open a command prompt in this directory
3. Run the following command:

```
docker-compose up -d
```

This will start MediaMTX in the background. The `-d` flag means "detached mode" (runs in the background).

## Configuration

- Edit `mediamtx.yml` to configure your camera streams
- For each camera, add a new entry under the `paths` section:

```yml
paths:
  camera1:
    source: rtsp://admin:password@camera_ip/ISAPI/Streaming/channels/101
```

- After changing the configuration, restart MediaMTX:

```
docker-compose restart
```

## Accessing Camera Streams

Once MediaMTX is running, your camera streams will be available at:

- RTSP: `rtsp://localhost:8554/camera1` (for software like VLC)
- HLS: `http://localhost:8888/camera1` (for web browsers)
- WebRTC: `http://localhost:8889/camera1` (for low-latency web viewing)

## Using with React Component

In your React application, use the MediaMTXStream component:

```tsx
<MediaMTXStream
  cameraIp="camera_ip"
  cameraChannel="101"
  rtspUsername="admin"
  rtspPassword="password"
  mediamtxApiUrl="http://localhost:9997"
  mediamtxHlsBaseUrl="http://localhost:8888"
/>
```

## Useful Commands

- Start MediaMTX: `docker-compose up -d`
- Stop MediaMTX: `docker-compose down`
- Restart MediaMTX: `docker-compose restart`
- View logs: `docker-compose logs -f`
- Check status: `docker-compose ps`

## Troubleshooting

- If streams aren't working, check your camera credentials and network connectivity
- Verify the camera is accessible from the server running Docker
- Check logs for errors: `docker-compose logs -f`
- Ensure all required ports are open (8554, 8888, 8889, 9997)
