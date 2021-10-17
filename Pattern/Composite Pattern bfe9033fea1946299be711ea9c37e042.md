# Composite Pattern

![Untitled](Composite%20Pattern%20bfe9033fea1946299be711ea9c37e042/Untitled.png)

- ViewNode 인터페이스
    
    이를 구현하는 2가지
    
    - Leaf 이거나
    - List<ViewNode> 이거나

[https://ko.wikipedia.org/wiki/컴포지트_패턴](https://ko.wikipedia.org/wiki/%EC%BB%B4%ED%8F%AC%EC%A7%80%ED%8A%B8_%ED%8C%A8%ED%84%B4)

```java
interface Graphic{
	public void print();
}

class Ellipse implements Graphic {
	public void print(){
		System.out.println("Ellipse");
	}
}

class CompositeGraphic implements Graphic {
	private List<Graphic> mChildGraphics = new ArrayList<Graphic>();
	
	public void print(){
		for(Graphic graphic : mChildGraphics) {
			graphic.print();
		}
	}
}
```