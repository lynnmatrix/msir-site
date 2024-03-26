---
modified: 2024-03-26T07:14:17.605Z
title: API Key
layout: post
nav_order: 3
---

# API Key
Api Key 用于在调用模型推理服务时的用户认证。
## 生成API Key
步骤：
1. `访问令牌` -> `新建访问令牌`
2. 填写令牌名称和有效期，名称便于区分不同的令牌，点击确认
3. 切记保存生成的令牌，之后该令牌不再被显示，服务器也没有记录。

## 使用API Key
下面分别以 curl 和 msir-infer SDK 为例，演示在调用推理服务时如何配置 API Key。

### Curl

{: .warning }
> *注意*：用自己生成的 API Key 替换下面示例中的 `${API_KEY}`。

buf curl http
``` sh
buf curl -H 'x-api-key: ${API_KEY}' --data '{"model_name": "product", "image_url": "https://someimage.jpg"}' --schema ./msir-infer/proto/apis/inference/v1/infer.proto -v http://localhost:9002/inference.v1.ImageInferenceService/InferImage
```

buf curl grpc
``` sh
buf curl --protocol grpc --http2-prior-knowledge -H 'x-api-key: ${API_KEY}' --data '{"model_name": "product", "image_url": "https://someimage.jpg"}' --schema ./msir-infer/proto/apis/inference/v1/infer.proto -v http://localhost:9003/inference.v1.ImageInferenceService/InferImage
```

grpcurl
``` sh
grpcurl -plaintext -H 'x-api-key: ${API_KEY}' -d '{"model_name": "product", "image_url": "https://someimage.jpg"}' -import-path ./msir-infer/proto -proto ./msir-infer/proto/apis/inference/v1/infer.proto localhost:9003 inference.v1.ImageInferenceService/InferImage
```

### SDK
TODO