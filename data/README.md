# IQ Recording

Download `Starlink_Downlink_IQ.csv` from the [v1.0.0 release](https://github.com/misaka666/Starlink-Downlink-Analysis/releases/download/v1.0.0/Starlink_Downlink_IQ.csv).

The CSV contains one header row, `I_data,Q_data`, followed by 11,520,180 sample rows. Each row represents one complex sample, `I + jQ`, at a sampling rate of 480 MHz. The recording duration is 24.000375 ms, and the file size is 311,026,556 bytes. Zero-based sample index `n` corresponds to relative time `n / 480000000` seconds.

The samples are complex-baseband receiver observations after downconversion and upstream coarse carrier synchronization. See the paper for the receiver processing used in the analysis.

## Integrity check

Place the downloaded CSV beside `SHA256SUMS`, then use:

```sh
sha256sum -c SHA256SUMS
```

On Windows PowerShell:

```powershell
Get-FileHash -Algorithm SHA256 -LiteralPath .\Starlink_Downlink_IQ.csv
```

Compare the result with `SHA256SUMS`.

## Example: load an initial portion

```python
import numpy as np

# Limit the example to the first 100,000 samples.
iq = np.loadtxt("Starlink_Downlink_IQ.csv", delimiter=",", skiprows=1,
                max_rows=100_000)
x = iq[:, 0] + 1j * iq[:, 1]
fs = 480_000_000
```

## 中文说明

`Starlink_Downlink_IQ.csv` 为复基带接收信号数据，表头为 `I_data,Q_data`，两列分别对应同相分量 I 和正交分量 Q。采样率为 480 MHz，共 11,520,180 个复采样点，时长为 24.000375 ms，文件大小为 311,026,556 字节。零基采样序号 `n` 对应的相对时间为 `n / 480000000` 秒。

数据为经过下变频和上游粗载波同步后的接收观测。论文介绍了分析中采用的接收处理方法。下载后请使用 `SHA256SUMS` 核对 SHA-256。
