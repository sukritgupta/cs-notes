#Meyer's Singleton  
Creates one object for class

> Prefer auto object creation rather than Pointer
> Return object by reference
> Use object by reference while calling
> No need to destroy(even static pointer)
> Make constructor private
> Delete Copy constructor and assignment operator (Optionally move constructor and move assignment operator also). 


```cpp
class singleton{
private:
	singleton(){};
	singleton(const singleton&) = delete;
	singleton& operator=(const singleton&) = delete;
  singleton(singleton&&) = delete;
  singleton& operator=(singleton&&) = delete;
  
public:	
	static singleton& instance(){
		static singleton obj;
		return obj;
	}
}

int main(){
  singleton& s = singleton::instance();
  return 0;
}
