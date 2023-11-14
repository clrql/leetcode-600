
  # online-stock-span

  ```golang
  type StockSpanner struct {
    prices []int
    spans  []int
}

func Constructor() StockSpanner {
    return StockSpanner{
        prices: make([]int, 0),
        spans:  make([]int, 0),
    }
}

func (this *StockSpanner) Next(price int) int {
    span := 1
    for len(this.prices) > 0 && price >= this.prices[len(this.prices)-1] {
        this.prices = this.prices[:len(this.prices)-1]
        span += this.spans[len(this.spans)-1]
        this.spans = this.spans[:len(this.spans)-1]
    }
    this.prices = append(this.prices, price)
    this.spans = append(this.spans, span)
    return span
}

/**
 * Your StockSpanner object will be instantiated and called as such:
 * obj := Constructor();
 * param_1 := obj.Next(price);
 */
  ```
  