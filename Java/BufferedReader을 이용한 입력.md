### ๐ฑโ๐ BufferedReader์ ์ด์ฉํ ์๋ ฅ

โ	Scanner๋ก ์๋ ฅ๋ฐ๋๋ค๊ณ  ํด๋ณด์. ์ ์ 10๊ฐ๋ฅผ ์๋ ฅ๋ฐ์ผ๋ ค๋ฉด `scanner ๊ฐ์ฒด์ nextInt()` ๋ฅผ ๋ฐ๋ณต๋ฌธ์ ํตํด 10๋ฒ ํธ์ถํด์ผํ๋ค. ์๋ ฅ ๊ฐฏ์๊ฐ ํฌ๋ฉด ๊ทธ๋งํผ ๋ฐ๋ณต๋ฌธ๋ ๋ง์ด ๋์์ ์๊ฐ์ด ๋ง์ด ๊ฑธ๋ฆฐ๋ค. 

โ	์ฐ๋ฆฌ๋ ์๋ ฅ์ ๋ฐ์ ๋ `System.in` ์ ํตํด ๋ฐ๊ฒ๋๋ค. in์ `InputStream` ํ์์ ๋ฉค๋ฒ๋ณ์์๋ค. `InputStream`์ ์๋ ฅ ์คํธ๋ฆผ์ผ๋ก๋ถํฐ 1๋ฐ์ดํธ๋ฅผ ์ฝ์ด์จ๋ค. ํ๋ฐ์ดํธ์ฉ ์ฝ๊ฒ๋๋ฉด 2๋ฐ์ดํธ์ธ ํ๊ธ์ ์๋ ฅํ๋ฉด ๋ฌธ์ ๊ฐ ์๊ธด๋ค. `InputStreamReader`์ ํ๋ฐ์ดํธ ๋จ์๋ก ์ฝ์ด์ค๋ ํ์์ ๋ฌธ์๋จ์๋ก ๋ณํ์์ผ์ค๋ค๊ณ  ํ๋ค. 

โ	๊ทธ๋ฌ๋ฉด `Scanner` ๊ฐ์ฒด์์ InputStream ํ์์ in ์ ํตํด ์๋ ฅ์ ๋ฐ๋๋ฐ ํ๋ฐ์ดํธ๋ง ๋ฐ๋๊ฑฐ ์๋๋๋ผ๊ณ  ์๊ฐ์ ํ๋๋ฐ `Scanner ์์ฑ์`๋ฅผ ํ๋ฒ ์ดํด๋ณด์๋ค. 

```java
public Scanner(InputStream source) {
        this(new InputStreamReader(source), WHITESPACE_PATTERN);
}
```

โ	Scanner (System.in (InputStream ํ์) ) ์์ฑ์๋ฅผ ํธ์ถํ๋ฉด ๋ด๋ถ์ ์ผ๋ก this(InputStreamReader, ~) ์์ฑ์๋ฅผ ํธ์ถํ๊ฒ ๋๋ค. ๊ทธ๋์ ํ๋ฐ์ดํธ๋ง ์ฝ๋ ๊ฒ์ด ์๋ ๋ฌธ์๋จ์๋ก ์ฝ์ด์ฌ ์ ์๋ค. 

โ	๋ค์ ๋์์์.. ํ ๋ฐ์ดํธ์ฉ ์ฝ์ด์ค๋ `InputStream`์ `InputStreamReader` ์ ํตํด ๋ ํจ์จ์ ์ผ๋ก ์๋ ฅ๋ฐ์์ฌ ์ ์๋ค. 

```java
	InputStreamReader isr = new InputStreamReader(System.in);
	char[] c = new char[10];
	sr.read(c);
	for(char str : c) {
        System.out.println(str);
    }
```

โ	InputStreamReader์ ๋ฌธ์๋ฅผ ์ฒ๋ฆฌํ๋ค. `BufferedReader`์ ํตํด ๋ฌธ์๋ค์ ์์๋ ํ ํ๋ฒ์ ๋ฌธ์์ด๋ก ์ฒ๋ฆฌํ๋ค. 

```java
	BufferedReader br = new BufferedReader(
    	new InputStreamReader(System.in)
    );
```

โ	`BufferedReader`์ ๋ฐ์ดํธ ํ์์ผ๋ก ์ฝ์ด๋ค์ด๋ in์ char๋ก ์ฒ๋ฆฌํ ๋ค String์ผ๋ก ์ ์ฅํ  ์ ์๋ค๊ณ  ํ๋ค. ๋ฒํผ๊ฐ ์๋ ์คํธ๋ฆผ์ด๊ณ  Scanner์ฒ๋ผ ์ ๊ท์์ ๊ฒ์ฌํ์ง ์๊ธฐ ๋๋ฌธ์ `Scanner์ ๋นํด ์ฐ์ํ๋ค` . BufferedReader๋ก ์๋ ฅ์ ๋ฐ์ ๋ ๋ค์๊ณผ ๊ฐ์ด ๋ฐ๋๋ค. 

```java
	BufferReader br = new BufferedReader(new InputStreamReader(System.in));
	try {
        String str = br.readLine();
    } catch(Exception e) {
        e.printStackTrace();
    }
```

### ๐ฑโ๐ ์ฐธ๊ณ ์๋ฃ

โ	1. [JAVA ์๋ ฅ ๋ฏ์ด๋ณด๊ธฐ](https://st-lab.tistory.com/41)