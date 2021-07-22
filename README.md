# Streaming media server using HTTP Live Streaming in Go

## Forked from the excellent tutorials by Lane Wagner at [QVault](https://dev.to/qvault/building-a-music-video-streaming-server-in-go-using-hls-216m) and [Rohir Mundra](https://rohitmundra.com/video-streaming-server)

### Requirements:
- [Go](https://golang.org/)
- [HTTP Live Streaming](https://developer.apple.com/documentation/http_live_streaming)
- [ffmpeg](https://www.ffmpeg.org/)
- [HLS.js](https://github.com/video-dev/hls.js/)


## How to run the demo


### Encode your media file
Navigate to the directory with a video or audio clip (I'm using an MP3 here) and encode it into HTTP Live Streaming chunks and a manifest using the H.264 codec:
- `ffmpeg -i BachGavotteShort.mp3 -c:a libmp3lame -b:a 128k -map 0:0 -f segment -segment_time 10 -segment_list outputlist.m3u8 -segment_format mpegts output%03d.ts`




### Compile & run the HTTP server
Start (or build) the server, which listens for requests on port 8080:
- `go run main.go`
- `go build -o server main.go` and then `./server` (or `./server.exe` for Windows)




### Test your server's endpoint
Ensure the contents of the manifest are being served:
- `curl -i  http://localhost:8080/BachGavotteShort/outputlist.m3u8`

### Preview your streaming media
Run the [HLS.js test client](https://hls-js-latest.netlify.com/demo/) and paste in the URL to your media manifest: [http://localhost:8080/BachGavotteShort/outputlist.m3u8](http://localhost:8080/BachGavotteShort/outputlist.m3u8)
