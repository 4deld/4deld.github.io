---
title: java lotto review
date: 2024-03-23 17:26:19 +0900
categories: [Alom Spring Course, POJO]
tags: [java]
seo:
  date_modified: 2024-04-10 17:46:53 +0900
---

## POJO(Plain Old Java Object)

Before we start to learn Spring, we were assigned the `POJO` task, an object designed in a way that is not dependent on the environment and technology, while remaining true to `object-oriented principles`, and can be recycled as needed. I thought this task was essential to learn Spring well and write codes that is `scalable and flexible to change`.

## [Java Lotto](https://github.com/4deld/java-lotto)

So, we studied POJO for two weeks, one assignment a week. first task was `Java Lotto`. Roughly, the task was to generate random numbers like a lottery and check if they matched the values entered by the user. I had to follow strict `object-oriented principles` and some `functional requirements` but it was difficult to write codes in accordance with the rules because I didn't know what exactly `OOP` is. I tried for about 20 hours but failed. Therefore I had no choice but to complete the assignment by copying `Kokodak`'s code.


## [Code Review](https://github.com/TEAM-ALOM/java-lotto/pull/13)

These are the `reviews` from one of my mentors.

> It would be better to have additional `unit tests` for other domains.

> View and Domain should be separated. `(MVC pattern)`

```Java
        validateBiggerThan0(Integer.parseInt(input));
    }
    private void validateInteger(final String input) {
        if (!(input.matches("[+-]?\\d*(\\.\\d+)?"))) {
```

It looks like a regular expression to verify whether it is a number, but I think it would be better to save the regular expression as an `NUMBER_REGEX` constant rather than hardcoding it.

```Java
            throw new IllegalArgumentException(NOT_A_NUMBER);
        }
    }
    private void validateBiggerThan0(final int amount) {
```

It's good that you wrote `the 0`, but it might be confused with `the O`, so I think it would be better to write it in `Zero`! or it would be good to show that it's a natural number test like a `validateNaturalNumber`.

```Java
        validateSix(numbers);
        validateDuplicatedNumber(numbers);
    }
    private void validateSix(List<Integer> numbers) {
```

If the number of lotto changes, shouldn't the method name change as well? This means `losing refactoring tolerance`.
I think we can change it like a `validateSize`.

```Java
        this.ticketNumber = amount / LOTTO_PRICE;
    }

    private void validateDivisibleBy1000(final int input) {
```

`validateDivisible` would be fine.

```Java
   public Lotto createNumbers() {
        List<Integer> randomNumbers = new ArrayList<>(
                Randoms.pickUniqueNumbersInRange(1, 45,
                        6));
        randomNumbers.sort(Comparator.naturalOrder());
        return new Lotto(randomNumbers);
    }
```

The method's name is `createNumbers`, but returning `the Lotto` doesn't seem appropriate. Also, `the LottoMachine` issues lottos according to the amount you put in, but it seems that the method of issuing only one lotto should not be exposed to `the outside world`.

```Java
   public class LottoMachine {
    private static final int LOTTO_PRICE = 1_000;

    private final List<Lotto> lottoArray = new ArrayList<>();
```

If you look at the `class name`, it seems that the focus was on lotto issuing. Therefore, does the class need to have the lottos information? The lottos seem to be good for the `Buyer` to own. I think it would be better to change class to the class that `simply issues lotto`. As an extension, it would be better to change the methods to `static`.

```Java
   public WinningNumbers(List<Integer> array, String bonusNumber) {
        validate(array,bonusNumber);
        this.array = array;
        this.bonusNumber=Integer.parseInt(bonusNumber);
    }
```

Just as Lotto received numbers as a `parameter`, it would be better for the class to receive `only numbers`. Validation that a string is a number must be done `outside` of its class. In the WinningNumbers class, it is contextually correct that `the numbers` are verified.

```Java
   import java.util.Arrays;

public enum MatchedPlace {
    ELSE(0,false,0),
```

`ELSE` is good, but I think naming `NONE` is also worth considering.  

```Java
public class Result {

    public static Map<MatchedPlace, Integer> getMatchedDetails(LottoArray lottoArray, WinningNumbers winningNumbers) {
```

If you give a `LottoArray`, additional dismantling process is required inside, and there is a hassle of making an additional LottoArray even when testing.
Why don't you get the parameters as `Lotto, WinningNumberers`?

```Java
    public static String readMoney() {
        System.out.println("구입금액을 입력해 주세요.");
        return Console.readLine();
    }
    public static List<Integer> readWinningArray() {
        System.out.println();
        System.out.println("당첨 번호를 입력해 주세요.");
        final String input = Console.readLine();

        return Parser.parseByDelimiter(input,",");
    }
    public static String readBonusNumber() {
        System.out.println();
        System.out.println("보너스 번호를 입력해 주세요.");
        return Console.readLine();
    }
```

I think it would be good to check if the value entered in is a number in `this section`.

## Feedback

This is the `feedback` that one of my mentors gave to people.

- Read `README.md` carefully. Some people are missing requirements or don't have a functional documentation.

- Think about `other exceptions` besides those listed. I think the basic of programming is `not to trust the client`. What if there were cases in which negative numbers were entered, or only strings were entered?

- Do not abbreviate `variable names`.

- Comply with `coding and committing conventions`.

- Use `Collection` rather than Array. Collection is good to utilize various `APIs`.

- View codes written by `others`. You can search, or see codes written by other team members. Implementation is important, but it's also very helpful to see and analyze codes written by others.

- Use `constants` without hardcoding.

- The overall writing of the `test codes` was lacking or inadequate. The test code is as important as `production code`, so be sure to write it during this week's mission.

## References

[Object Calisthenics](https://jamie95.tistory.com/99)

[Unit test1](https://mangkyu.tistory.com/143)

[Unit test2](https://mangkyu.tistory.com/144)


My English might be awkward. If you have any inconvenience, please send me an email so that I can correct it.

Email: deld4@icloud.com

Thank you for reading my post.

