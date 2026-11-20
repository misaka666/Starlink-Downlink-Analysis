# Raw IQ / 原始IQ

[Download / 下载：Starlink_Downlink_IQ_250MSps.bin](https://github.com/misaka666/Starlink-Downlink-Analysis/releases/download/v2.0.0/Starlink_Downlink_IQ_250MSps.bin)

250 MS/s · 12,500,000 complex samples / 复样本 · 50 ms · 50,000,000 bytes.

Little-endian signed int16, interleaved I,Q. / 小端有符号int16，I、Q交替排列。
This original recording contains nine complete validated frames plus other candidates and a truncated frame. / 原始记录包含9个完整已验证帧，另有其他候选信号和截断帧，并非恰好9帧连续信号。

SHA-256: `c69e82022d45173cdcaf1a5fdc8a2b864e2d61e85ae819af54b16002044adae3`

```python
import numpy as np
iq = np.fromfile('Starlink_Downlink_IQ_250MSps.bin', dtype='<i2').reshape(-1, 2)
x = iq[:, 0].astype(np.float32) + 1j * iq[:, 1].astype(np.float32)
```

```matlab
fid = fopen('Starlink_Downlink_IQ_250MSps.bin','rb','ieee-le');
iq = fread(fid,[2 Inf],'int16=>double'); fclose(fid);
x = complex(iq(1,:),iq(2,:)); Fs = 250e6;
```

[Frame validation / 逐帧验证](frames_9.csv) · [PDU decoded words / PDU译码字](pdu_headers_9.csv) · [Validation scope / 验证范围](validation_9frames.json)
