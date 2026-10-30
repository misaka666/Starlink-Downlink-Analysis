# Starlink Downlink Analysis

Research materials accompanying **Protocol Data Unit Header Decoding and Payload Coding Recovery in the Starlink Ku-Band Downlink**.

This repository provides an English research manuscript, Chinese and English technical articles, and an IQ recording from the analyzed continuous capture.

## Paper and technical articles

- [English paper (PDF)](paper/Starlink_Downlink_Analysis.pdf)
- [English technical article](docs/Starlink_Downlink_Analysis_EN.md)
- [中文技术文章：星链下行信号格式解析](docs/Starlink_Downlink_Analysis_ZH.md)

The articles cover the frame grid, two protocol data unit (PDU) headers, header convolutional coding and CRC, candidate modulation and coding scheme (MCS) fields, payload allocations, and recovered channel-coding relations. They include a complete resource map and received constellations for frame R02.

## Download the IQ recording

**[Download Starlink_Downlink_IQ.csv](https://github.com/misaka666/Starlink-Downlink-Analysis/releases/download/v1.0.0/Starlink_Downlink_IQ.csv)** · [Release v1.0.0](https://github.com/misaka666/Starlink-Downlink-Analysis/releases/tag/v1.0.0)

The CSV is distributed as a release asset rather than a regular Git file. Cloning this repository does not download the IQ recording.

| Property | Value |
| --- | --- |
| Columns | `I_data`, `Q_data`, in that order |
| Header | One header row |
| Sample rate | 480,000,000 samples/s |
| Complex samples | 11,520,180 |
| Duration (`samples / sample rate`) | 24.000375 ms |
| File size | 311,026,556 bytes |
| Sample representation | Decimal text, with the original stored I/Q values preserved |
| Recording stage | Complex baseband after downconversion and upstream coarse carrier synchronization |
| Time column | Omitted; sample index determines relative time |

The recording was stored in three consecutive numbered segments. They have been concatenated in numerical order into one continuous recording, without reordering or resampling the I/Q values. The two columns form `I + 1j * Q`.

See [data documentation](data/README.md), [metadata](data/metadata.json), and [SHA-256 checksum](data/SHA256SUMS).

## Scope of the results

The manuscript analyzes 18 complete frames from one continuous capture. It reports recovered header coding and CRC, a conditional 20-bit MCS index–length layout, and several receiver-equivalent payload coding relations. The seven-bit-index-plus-one-bit and eight-bit-index interpretations remain indistinguishable in this recording; a 19-bit alternative has not been uniquely excluded.

Codes 28 and 37 have verified shortened coding cores, with 256 and 384 additional observed bits still unexplained. Code 68 remains unresolved. Some observations participated in model selection. Exclusion from generator fitting is therefore not a claim of wholly unseen validation data, and these results do not constitute application-payload recovery or complete protocol identification.

## 中文说明

本仓库包含英文论文、中英文技术文章及一段连续采集的星链下行 IQ 数据。数据为两列 CSV，依次是 I、Q，不含时间列，采样率 480 MHz。完整 CSV 请通过上方 Release 链接下载，普通 `git clone` 不包含该文件。

文章重点介绍帧结构、PDU 头部、CRC、MCS 字段与载荷编码。条件性布局、尚未解释的比特和未恢复编码均在文稿中注明。
