#### FFMPEG to compress mp4 video
ffmpeg -i automa.mp4 -vcodec libx265 -crf 28 output.mp4