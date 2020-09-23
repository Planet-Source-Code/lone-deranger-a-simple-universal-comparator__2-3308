<div align="center">

## A simple universal comparator


</div>

### Description

You can use this class to sort an array of Objects without creating custom Comparators for each field. For example, if you have a class Employee, with methods getName() and getSalary(), you can simply do Arrays.sort(myEmployeeArray, new UniversalComparator("getName", 1)) or Arrays.sort(myEmployeeArray, new UniversalComparator("getSalary", -1)). The first statement would sort your array in ascending order by the value of getName() method, the second would sort it in descending order by the value of getSalary() method. The class uses the reflection API to accomplish this task.
 
### More Info
 
You need to import java.util.Arrays, java.util.Comparator in order to use Arrays.sort(). The return value of your Object's methods MUST implement the Comparable interface.


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Lone Deranger](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/lone-deranger.md)
**Level**          |Advanced
**User Rating**    |5.0 (10 globes from 2 users)
**Compatibility**  |Java \(JDK 1\.1\), Java \(JDK 1\.2\)
**Category**       |[Classes](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/classes__2-83.md)
**World**          |[Java](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/java.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/lone-deranger-a-simple-universal-comparator__2-3308/archive/master.zip)





### Source Code

```
import java.lang.Object;
import java.lang.reflect.*;
import java.util.Comparator;
public class UniversalComparator extends Object implements Comparator {
	private String methodName = "toString";
	private int descAscIndicator = 1;
	public static final int ASCENDING = 1;
	public static final int DESCENDING = -1;
	public UniversalComparator(int descAscIndicator) {
		this.descAscIndicator = descAscIndicator;
	}
	public UniversalComparator(String methodName, int descAscIndicator) {
		this(descAscIndicator);
		this.methodName = methodName;
	}
	public int compare(Object o1, Object o2) {
		Object comp1 = null;
		Object comp2 = null;
		try {
		Method o1_Method = o1.getClass().getMethod(methodName, null);
		Method o2_Method = o2.getClass().getMethod(methodName, null);
		comp1 = o1_Method.invoke(o1, null);
		comp2 = o2_Method.invoke(o2, null);
		} catch (NoSuchMethodException e) {
		} catch (IllegalAccessException e) {
		} catch (InvocationTargetException e) {}
		Comparable c1 = (Comparable) comp1;
		Comparable c2 = (Comparable) comp2;
		return c1.compareTo(c2) * descAscIndicator;
	}
	public boolean equals(Object obj) {
		return this.equals(obj);
	}
}
```

