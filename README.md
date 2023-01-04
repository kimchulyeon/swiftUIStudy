# swfitUI

## 🥑 기본 형태 배우기

텍스트 띄워보기
```
import SwiftUI

struct ContentView: View {

  var body: some View {
    Text("Hello world")
      .font(.largeTitle)
      .foregroundColor(.green)
  }
}
```

subView로 빼기 : 리액트처럼 컴포넌트 분리 개념
- 커맨트 + 클릭 => extrach subview

```
struct ContentView: View {
  let hikes: Hike.all()
  
  var body: some View {
    List(hikes, id: \.name) { hike in
      HikeCell(hike: hike)
    }
  }
}

// 📌 분리한 subview
struct HikeCell: View {
  let hike: Hike

  HStack {
    Image(hike.imageUrl)
      .resizable()
      .aspectRatio(contentMode: .fit)
      .frame(width: 100, height: 100)
      .cornerRadius(20)
    Text(hike.name)
  }
}
```
