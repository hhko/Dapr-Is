
## HTTP 통신 Helloworld 예제

```cs
using Dapr.Client;

// WebAPI 클라이언트
class Program
{
    static async Task Main(string[] args)
    {
        using var client = new DaprClientBuilder().Build();
        var message = await client.InvokeMethodAsync<string>("app2", "hello", "Hello from app1!");
        Console.WriteLine($"Response from app2: {message}");
    }
}
```
- InvokeMethodAsync 메서드
  - `"app2"` : 첫 번째 매개변수는 대상 애플리케이션의 ID입니다.
  - `"hello"` -> `[HttpPost("hello")]` : 두 번째 매개변수는 호출할 메서드의 이름입니다.
  - `"Hello from app1!"` -> `[FromBody] string message` : 세 번째 매개변수는 호출할 메서드의 인수입니다.

```cs
using Dapr;

// WebAPI 서버
public class HelloController : ControllerBase
{
    [HttpPost("hello")]
    public ActionResult<string> SayHello([FromBody] string message)
    {
        return Ok($"Hello from app2! Received message: {message}");
    }
}
```