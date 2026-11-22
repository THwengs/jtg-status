# jtg-status

客户端远程状态开关用的签名文件。由 `status-sign.py` 生成，**不要手改**。

- `status.json` — 当前状态（RSA-2048 / SHA-256 签名）
- 客户端用安装包里内嵌的 `status_pub.pem` 验签

## 字段说明

| 字段 | 含义 |
|---|---|
| `revoke_all` | `true` = 所有客户机停服 |
| `revoked_codes` | 只停这些授权码 |
| `valid_until` | 到这个时间后全部停服 |
| `signature` | 对「去掉 signature 后的规范化 JSON」的签名 |

## 生成方式（本机，勿在服务器上跑）

```bash
python tools/status-sign.py --ok
python tools/status-sign.py --revoke-all
python tools/status-sign.py --revoke <码1>,<码2>
python tools/status-sign.py --clear
```

生成后把 `status.json` 覆盖到这里并提交即可，客户端 1~5 分钟内生效。
