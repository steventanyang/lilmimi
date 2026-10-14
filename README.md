# LilMimi

I built this to understand [Mimi](https://github.com/kyutai-labs/moshi), the neural audio
codec at the heart of Kyutai's Moshi.


## Run it

```bash
uv sync
uv run python mic.py            # record 4s, round-trip it, play both back
uv run python bench.py          # per-stage latency against the 80 ms budget
```

## Latency

```
  stage                       min      p50      p95
  --------------------------------------------------
  encode seanet              5.85     6.35     6.78
  encode transformer         8.59    11.70    14.08
  encode downsample          0.13     0.14     0.20
  quantize                   1.73     2.41     3.28
  dequantize                 0.49     0.52     1.34
  decode upsample            1.06     1.08     1.25
  decode transformer         8.29    10.70    13.04
  decode seanet              6.83     7.39     8.08
  TOTAL                     35.20    39.41    46.84

  budget 80 ms   using 44%   headroom 44.8 ms   2.27x realtime
```