# WordCountLib
Create by: Денис Казанцев & Артем Николаев

-lib

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Text.RegularExpressions;
    using System.Threading.Tasks;
    using static System.Net.Mime.MediaTypeNames;
    
    namespace WordCountLib1
    {
    /// <summary>
        /// Метод принимает две строки: textString и word. Строка textString содержит исходный текст, строка word представляет собой слово, которое нужно искать.
        /// Для упрощения задачи гарантируется, что переменная textString содержит только буквы и пробелы;
        /// Значение переменной word всегда состоит из букв и содержит по крайней мере два символа.
        /// </summary>
        /// <param name="textString"></param>
        /// <param name="word"></param>
        /// <returns>
        /// Метод возвращает целое число - количество слов word в тексте textString.
        ///</returns>
        /// <exception cref="Exception"></exception>
        public class WordCounts
        {
            public static int WordCount(string textString, string word)
            {
                if (word.Length <= 1)
                {
                    throw new Exception("Слишком короткое слово");
                }
                if (string.IsNullOrWhiteSpace(textString) || string.IsNullOrWhiteSpace(word))
                {
                    throw new Exception("Строка пуста");
                }
                int count = Regex.Matches(textString.ToLower(), word.ToLower()).Count; 
                return count;
            }
    
    
        }
    }
-tests

    using Microsoft.VisualStudio.TestTools.UnitTesting;
    using System;
    using WordCountLib1;
    
    namespace WordCountTests
    {
        [TestClass]
        public class WordCountLibTests
        {
            /// <summary>
            /// Подсчет количества слов в строке
            /// </summary>
            [TestMethod]
            public void Test_CheckQuantityOfWord()
            {
                string textString = "Мама мама мама";
                string word = "мама";
                int actual = WordCounts.WordCount(textString, word);
                Assert.AreEqual(actual, 3);
            }
            /// <summary>
            /// Проверка на отсутствие слова в строке
            /// </summary>
            [TestMethod]
            public void Test_CheckWithoutWord()
            {
                string textString = "File is not finde";
                string word = "nig";
                int actual = WordCounts.WordCount(textString, word);
                Assert.AreEqual(actual, 0);
            }
            /// <summary>
            /// подсчет слов вне зависимости от регистра
            /// </summary>
            [TestMethod]
            public void Test_IndependRegister()
            {
                string textString = "Мамfа мАа мама";
                string word = "маа";
                int actual = WordCounts.WordCount(textString, word);
                Assert.AreEqual(actual,1);
            }
            /// <summary>
            /// Проверка на короткое слово
            /// </summary>
            [TestMethod]
            public void Test_ShortWord()
            {
                string textString = "Мамfа маа мама";
                string word = "м";
                Action actual = () => WordCounts.WordCount(textString, word);
                Assert.ThrowsException<Exception>(actual);
            }
            /// <summary>
            /// Пустая строка
            /// </summary>
            [TestMethod]
            public void Test_EmptyString()
            {
                string textString = "";
                string word = "ма";
                Action actual = () => WordCounts.WordCount(textString, word);
                Assert.ThrowsException<Exception>(actual);
            }
            /// <summary>
            /// Пустая нижняя строка
            /// </summary>
            [TestMethod]
            public void Test_EmptyUpperString()
            {
                string textString = "Мамfа маа мама";
                string word = "";
                Action actual = () => WordCounts.WordCount(textString, word);
                Assert.ThrowsException<Exception>(actual);
            }
    
            /// <summary>
            /// Строка из Пробелов нижняя
            /// </summary>
            [TestMethod]
            public void Test_SpaceLowerString2()
            {
                string textString = "Мамfа маа мама";
                string word = "   ";
                Action actual = () => WordCounts.WordCount(textString, word);
                Assert.ThrowsException<Exception>(actual);
            }
            /// <summary>
            /// Строка из Пробелов верхняя
            /// </summary>
            [TestMethod]
            public void Test_EmptyUpperString3()
            {
                string textString = "        ";
                string word = "маа";
                Action actual = () => WordCounts.WordCount(textString, word);
                Assert.ThrowsException<Exception>(actual);
            }
        }
    }

