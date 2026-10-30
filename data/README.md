# IQ Recording

Download the original CSV from the [v1.0.0 release](https://github.com/misaka666/Starlink-Downlink-Analysis/releases/download/v1.0.0/Starlink_Downlink_IQ.csv).

`Starlink_Downlink_IQ.csv` contains a header followed by 11,520,180 rows. The columns are `I_data,Q_data`. One row represents one complex sample, `I + jQ`, at 480 MHz. Duration is 24.000375 ms. The time column has been removed; the relative time of zero-based sample `n` is `n / 480000000` seconds.

Three numbered storage segments were concatenated in order. No samples were inserted, removed, resampled, or converted to a new numeric precision. Only the original time column and repeated segment headers were removed. The final CSV has a single `I_data,Q_data` header.

## Integrity check

Place the downloaded CSV beside `SHA256SUMS`, then use:

```sh
sha256sum -c SHA256SUMS
```

On Windows PowerShell:

```powershell
Get-FileHash -Algorithm SHA256 -LiteralPath .\Starlink_Downlink_IQ.csv
```

Compare with `SHA256SUMS`. File size is 311,026,556 bytes.

## Example: load an initial portion

```python
import numpy as np

# Limit the example to the first 100,000 samples.
iq = np.loadtxt("Starlink_Downlink_IQ.csv", delimiter=",", skiprows=1,
                max_rows=100_000)
x = iq[:, 0] + 1j * iq[:, 1]
fs = 480_000_000
```

These are received baseband samples. The receiver corrections and PN reference-phase removal described in the paper have not been newly applied while assembling this CSV.

## 中文说明

CSV 按原始编号顺序拼接，仅保留 I、Q 两列和一次表头。采样率为 480 MHz，11,520,180 个复采样点，总时长 24.000375 ms。去掉时间列后，可由采样序号恢复相对时间。本次拼接未执行重采样、均衡或 PN 参考相位去除。下载后请核对 SHA-256。
