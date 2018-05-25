# Tips . Tricks . Optimization

---
NOTE:
- New items will be added at the top with descending numbering. 
- If a new code is needed to be added at the middle, number it as ‘10.1’ or ‘10.a’ etc. Do not change any existing number.
---

## [1]
Optimization by compiler <br/>
Ref: https://stackoverflow.com/questions/1749966/c-sharp-how-to-determine-whether-a-type-is-a-number
````c#
public static bool IsNumericType(Type type)
{
  switch (Type.GetTypeCode(type))
  {
	case TypeCode.Byte:
	case TypeCode.SByte:
	case TypeCode.UInt16:
	case TypeCode.UInt32:
	case TypeCode.UInt64:
	case TypeCode.Int16:
	case TypeCode.Int32:
	case TypeCode.Int64:
	case TypeCode.Decimal:
	case TypeCode.Double:
	case TypeCode.Single:
  	return true;
	default:
  		return false;
  }
}
````
Compiler will optimize and generate below IL. Moreover the above code is more readable, leave rest to the IL.
````c#
public static bool IsNumericType(Type type)
{
  TypeCode typeCode = Type.GetTypeCode(type);
  //The TypeCode of numerical types are between SByte (5) and Decimal (15).
  return (int)typeCode >= 5 && (int)typeCode <= 15;
}
````
