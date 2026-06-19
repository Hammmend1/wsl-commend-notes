# Mirror Windows network to WSL

1. Create a file named `.wslconfig` in `%USERPROFILE%`.
2. Add the following content:

``` ini
[wsl2]
networkingMode=mirrored
autoProxy=true
