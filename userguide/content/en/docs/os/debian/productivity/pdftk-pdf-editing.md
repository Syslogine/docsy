---
title: "Creating and Editing PDFs with PDFtk"
description: "Instructions for using PDFtk (PDF Toolkit) to create and edit PDF documents, merge PDF files, and perform other PDF manipulation tasks on Debian systems."
icon: "code"
draft: false
toc: true
weight: 1
---

## Introduction

PDFtk, short for PDF Toolkit, is a command-line tool that allows you to perform various operations on PDF documents, including merging, splitting, encrypting, decrypting, and more. In this tutorial, you will learn how to use PDFtk to create and edit PDF documents on Debian systems.

## Installation

1. Open a terminal on your Debian system.
2. Install PDFtk by running the following command:
   ```
   sudo apt update
   sudo apt install pdftk
   ```
3. Once the installation is complete, you can start using PDFtk from the command line.

## Creating PDF Documents

1. To create a new PDF document using PDFtk, you can use the `cat` command to concatenate text files or use the `echo` command to generate text.
   ```
   echo "Hello, world!" | pdftk - output hello.pdf
   ```
2. This command will create a new PDF document named `hello.pdf` with the text "Hello, world!".

## Editing PDF Documents

1. PDFtk allows you to edit existing PDF documents by adding, removing, or modifying pages.
2. To add pages from another PDF document to an existing PDF, you can use the `cat` operation.
   ```
   pdftk input1.pdf input2.pdf cat output combined.pdf
   ```
   This command will combine pages from `input1.pdf` and `input2.pdf` into a new PDF named `combined.pdf`.
3. You can also remove pages from a PDF document using the `cat` operation with the `~` symbol to exclude specific pages.
   ```
   pdftk input.pdf cat 1-4 7-end output trimmed.pdf
   ```
   This command will create a new PDF named `trimmed.pdf` containing pages 1 through 4 and all pages after page 7 from the original `input.pdf`.
4. Additionally, you can rotate pages, stamp watermarks, and encrypt PDF documents using PDFtk.

## Merging PDF Files

1. To merge multiple PDF files into a single PDF document, you can use the `cat` operation with multiple input files.
   ```
   pdftk file1.pdf file2.pdf cat output merged.pdf
   ```
   This command will merge `file1.pdf` and `file2.pdf` into a new PDF named `merged.pdf`.
2. You can specify the order of the input files to control the page sequence in the merged PDF.

## Conclusion

PDFtk is a powerful tool for creating and editing PDF documents on Debian systems. By following this tutorial, you should now be able to install PDFtk, create new PDF documents, edit existing PDFs, merge PDF files, and perform other PDF manipulation tasks using PDFtk commands in the terminal.
