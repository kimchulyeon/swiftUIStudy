# swiftUI

[텍스트 띄워보기](https://github.com/kimchulyeon/mySwiftStudy/blob/main/README.md#-텍스트-띄워보기)
[subView로 분리](https://github.com/kimchulyeon/mySwiftStudy/blob/main/README.md#-subview로-빼기-리액트처럼-컴포넌트-분리-개념)
[NavigationView](https://github.com/kimchulyeon/mySwiftStudy/blob/main/README.md#-navigationview)
[List](https://github.com/kimchulyeon/mySwiftStudy/blob/main/README.md#-list)

<br />

### 🥑 텍스트 띄워보기

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

<br />

### 🥑 subView로 빼기 : 리액트처럼 컴포넌트 분리 개념

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

// 📌 분리한 subview | 파일로 분리해도 된다
struct HikeCell: View {
  let hike: Hike

  HStack {
    Image(hike.imageUrl)
      .resizable()
      .aspectRatio(contentMode: .fit)
      .frame(width: 100, height: 100)
      .cornerRadius(20)
    VStack(alignment: .leading) {
      Text(hike.name)
      Text(String(format: "%.2f", hike.miles))
    }
  }
}
```

<br />

### 🥑 NavigationView

전체를 씌운다

navigationTitle이랑 navigationBarTitleDisplayMode는 NavigationView {} 블록이 아니라 설정할 뷰 {} 블록 뒤에 위치

```
struct ContentView: View {
  //MARK: - properties
  let hikes = Hike.all()

  var body: some View {
    NavigationView {
      List(hikes, id: \.name) { hike in
        NavigationLink {
          HikeDetail(hike: hike)
        } label: {
          HikeListItem(hike: hike)
        }
      }

      .navigationTitle("Hikings")
      .navigationBarTitleDisplayMode(.inline)
    } 
  }
}
```

### 🥑 List

```
let 어떤 데이터 = [["1", "2"], ["3", "4", "5"], ["ㅁㅇㄹㅁㅇㄹ", "ㅁㄴㅇ러ㅗㅁㄴㅇㄹ", "아ㅓㅗ니푸"]]

List(어떤 데이터, id: 데이터고유값) { 데이터 아이템 in
  ForEach(데이터 아이템, id: 데이터 아이템 고유값) { 데이터 아이템의 아이템 in 
    Text(데이터 아이템의 아이템.text)
  }
}
```

::::::::::::::::::::::::::::::결과::::::::::::::::::::::::::::::

![image](https://user-images.githubusercontent.com/86825214/210679366-23c9ecdd-0e81-43ca-bd3f-892a384a7ef6.png)

어떤 데이터가 배열 속의 배열이 있기 때문에 List안에 ForEach()로 배열 속 배열을 순환

<br />

### 🥑 배열 속 배열 아이템 리스트

Hstack으로 임베드해서 하나의 리스트안에 수평으로 텍스트를 그린다
```
let images = [["1", "2"], ["3", "4", "5"], ["ㅁㅇㄹㅁㅇㄹ", "ㅁㄴㅇ러ㅗㅁㄴㅇㄹ", "아ㅓㅗ니푸"]]

List(images, id: \.self) { image in
  HStack {
    ForEach(image, id: \.self) { item in
      Text(item)
    }
  }
}
```

<br />

### 🥑 LazyVGrid

LazyVGrid의 columns인자는 \[GridItem] 이여야한다.

다양한 \[GridItem] 형태

- Array(repeating: GridItem(.flexible(), spacing: 5), count: 3) 
- \[GridItem(.fixed(100)), GridItem(.fixed(100)), GridItem(.fixed(100))]
- \[GridItem(.flexible(minimun: 10, maximun: 100)), GridItem(), GridItem(.fixed(50))]
- \[GridItem(.adaptive(minimun: 100, maximun: 120)), GridItem(.fixed(100)), GridItem(.fixed(100))]

```
let images = ["1", "2", "3", "4", "5", "ㅁㅇㄹㅁㅇㄹ", "ㅁㄴㅇ러ㅗㅁㄴㅇㄹ", "아ㅓㅗ니푸"]

let myColumns: [GridItem] = Array(repeating: GridItem(.flexible(), spacing: 10), count: 3)

LazyVGrid(columns: myColumns, spacing: 20) {
  ForEach(images, id: \.self) { image in
    Text(image)
  }
}
```
