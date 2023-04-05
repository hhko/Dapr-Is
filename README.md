## 목차
- **개발 환경**
  - Chocolatey
  - .NET 7+
  - Visual Studio Code
  - PowerShell 7+
  - Windows Terminal
  - Docker Desktop
  - WSL2
  - Tye
- **Dapr Docs**
  - Dapr 개념 Concepts
    - Sidecar 패턴
    - Dapr 설치
    - Hello world 예제
  - Dapr 시작하기 Getting Started
    - Dapr 설치
      - [Dapr CLI 설치](./DaprDocs/Part2_GettingStarted/Ch01_InstallDaprCli/)
      - [Dapr Runtime 초기화](./DaprDocs/Part2_GettingStarted/Ch02_InitializeDapr/)
    - Dapr Helloworld 예제
      - [Dapr Hello Sidecar 예제](./DaprDocs/Part2_GettingStarted/Ch03_HelloSidecar/)

<br/>

## HTTP 통신 Hello world 예제

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

## 참고 자료
- [ ] https://docs.dapr.io/
- [ ] https://learn.microsoft.com/ko-kr/dotnet/architecture/microservices/
- [ ] https://github.com/EdwinVW/dapr-traffic-control
- [ ] https://github.com/EdwinVW/dapr-workshop
- [ ] https://github.com/dotnet-architecture/eShopOnDapr?WT.mc_id=dotnet-35129-website
---
- [ ] https://qiita.com/kazumihirose/items/f7811bf3e5abe405a551
- [ ] https://bitoftech.net/2022/08/25/tutorial-building-microservice-applications-azure-container-apps-dapr/
- [ ] https://swoopfunding.com/swoop-engineering/microservices-with-dapr-mini-series-pub-sub-tye/
- [ ] https://blog.csdn.net/sD7O95O/article/details/120499674
- [ ] https://visualstudiomagazine.com/articles/2022/05/03/dapr-workshop.aspx
- [ ] https://www.youtube.com/watch?v=TeHVd3UlfY8
- [ ] https://www.youtube.com/watch?v=g-gOlkD9lKs
- [ ] https://www.youtube.com/watch?v=kIfmwmJHNMs
