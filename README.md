# NYC Road Safety — backdrop strips

The animated frame strips of the NYC Road Safety dashboard (BoldVizRight), served over https for Tableau Web Page objects (NG1, 2026-11-02; the NSW E5 route). Six cover pages, each playing `<strip>.webm` / `.mp4` (125 frames at 12.5 fps, encoded from the design tool's GIFs over the page ground `#F6F7FB`) behind a JPEG poster; the Executive's top and bottom strips serve both dashboards (1680 × 144); the sides are 120 × 1318 (Executive) and 120 × 2386 (Operational, stretched from the tool's 1317-px export).

    ffmpeg -i <strip>.gif -filter_complex "[0:v]format=rgba,scale=W:H:flags=lanczos[g];color=c=0xF6F7FB:s=WxH:r=12.5[bg];[bg][g]overlay=shortest=1:format=auto,format=yuv420p[v]" -map "[v]" -r 12.5 -c:v libvpx-vp9 -b:v 0 -crf 38 -deadline good -cpu-used 2 -row-mt 1 -an <strip>.webm
    ffmpeg ... -c:v libx264 -preset slow -crf 26 -movflags +faststart -an <strip>.mp4
    ffmpeg ... -frames:v 1 -q:v 3 <strip>-poster.jpg
