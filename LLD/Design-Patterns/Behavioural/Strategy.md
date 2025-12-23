# Strategy Design Pattern

>Strategy pattern encapsulates interchangeable algorithms behind a common interface and lets the behavior of an object change at runtime without modifying its code.
- At runtime we decide strategy to consider which class variant.

Wrong Implementation will have if else ladder, which is highly coupled. 

```cpp
class PricingEngine {
public:
    double calculatePrice(string customerType, double amount) {
        if (customerType == "REGULAR")
            return amount;
        else if (customerType == "PREMIUM")
            return amount * 0.9;
        else if (customerType == "VIP")
            return amount * 0.8;
        return amount;
    }
};

```

----------
## Strategy
```cpp
class PricingStrategy{
  public:
  virtual double calculate(double amount) const = 0;
  virtual ~PricingStrategy() = default;
};

class RegularPricing: public PricingStrategy{
public:
    double calculate(double amount) const override {
    return amount;
  }
};

class PremiumPricing: public PricingStrategy{
public:
    double calculate(double amount) const override {
    return amount*0.9;
  }
};

class VIPPricing: public PricingStrategy{
public:
    double calculate(double amount) const override {
    return amount*0.8;
  }
};
```
## Context
```cpp
class PricingEngine{
  PricingStrategy* strategy_;
public:
  PricingEngine(PricingStrategy* strategy):strategy_(strategy){}
  double calculate(double amount) const{
    return strategy_->calculate(amount);
  }
};
```
## Usage
```cpp
int main(){
  double amount  = 100000;
  PremiumPricing premPrice;
  PricingStrategy* strategy = &premPrice;
  PricingEngine pricingEng(strategy);
  pricingEng.calculate(amount);
  return 0;
}
```
