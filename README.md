
# GPT-5.1 Yeni Araç Tipleri

## apply_patch

apply_patch, GPT-5.1’in ek tanım gerektirmeden gerçek dosya değişiklikleri yapabildiği, adım adım çalıştığı ve freeform çağrılar sayesinde hata oranını azaltan bir kod düzenleme aracıdır.

```python
response = client.responses.create(
    model="gpt-5.1",
    input=RESPONSE_INPUT,
    tools=[{"type": "apply_patch"}]
)
```

### *apply_patch* aracı çağrıldığında yanıt akışında alabileceğimiz fonksiyon tipi

```python
{
    "id": "apc_08f3d96c87a585390069118b594f7481a088b16cda7d9415fe",
    "type": "apply_patch_call",
    "status": "completed",
    "call_id": "call_Rjsqzz96C5xzPb0jUWJFRTNW",
    "operation": {
        "type": "update_file",
        "diff": "
        @@
        -def fib(n):
        +def fibonacci(n):
        if n <= 1:
            return n
        -    return fib(n-1) + fib(n-2)                                                  
        +    return fibonacci(n-1) + fibonacci(n-2)",
    "path": "lib/fib.py"
    }
},

```

### Responses API'ının beklediği çıktı formatı

```python
{
    "type": "apply_patch_call_output",
    "call_id": call["call_id"],
    "status": "completed" if success else "failed",
    "output": log_output
}

```

---

## Komut Satırı Aracı *shell tool*

GPT-5.1 shell tool, modelin bilgisayarda komut çalıştırarak veri toplamasını ve görevleri tamamlamasını sağlayan kontrollü bir araçtır.

```python
tools = [{"type": "shell"}]

```

### *shell* aracı çağrıldığında yanıt akışında alabileceğimiz fonksiyon tipi

```python
{
 "type": "shell_call",
 "call_id": "...", 
 "action": {
  "commands": [...], 
  "timeout_ms": 120000,
  "max_output_length": 4096 
 },
 "status": "in_progress"
}
```

### Shell komutu çalıştığında dönen değerler

```python
{
 "type": "shell_call_output",
 "call_id": "...", 
 "max_output_length": 4096, 
 "output": [
  {
   "stdout": "...", 
   "stderr": "...", 
   "outcome": {
    "type": "exit", 
    "exit_code": 0
   } 
  }
 ] 
}
```
