---
author: tttwrites
comments: true
date: 2014-09-13 06:01:16+00:00
layout: post
slug: file-copy-program-using-pipe-between-parent-and-child-process-in-c
title: File copy program using pipe between parent and child process in C
wordpress_id: 644
categories:
- FOSS
- Operating Systems
tags:
- c pipe
- c program to copy file
- child parent pipe
- copy between parent child
- fie copy program
---

Starting the Operating Systems 'category' with this program.
Problem statement:- 
**Design a file copying program named FileCopy using ordinary pipes. This program will be passed two parameters : the first is the name of the file to be copied and the second is the name of the copied file. The program will then create an ordinary pipe and write the contents of the file to be copied to the pipe. The child process will read this file from the pipe and write it to the destination file. **
For example, if we invoke the program as follows 
FileCopy input.txt copy.txt 
Solution:
[code language="C"]
#include<stdio.h>
#include<sys/types.h>
#include<sys/stat.h>
#include<fcntl.h>
#include<string.h>
#include<stdlib.h>

int main( int argc, char* argv[] ) {
	int fdone[2];
	pid_t childid;

	char readBuff[50];
	char writeBuff[50];
	int readCounter;

	pipe( fdone );

	if( argc < 3 ) {
	    printf( "Atleast need 2 params " );
	    exit(1);
	}

	int fileOpen = open( argv[1], 0 );
	int targetFile = open( argv[2], 0666 );
	
	if ( fileOpen == -1 || targetFile == -1 ) {
	    printf( "Opening file failed " );
	    exit(1);
	}
	childid = fork();

	if( childid == 0 ) {
	    // inside the child prcocess
	    close( fdone[1] );

	    read( fdone[0], readBuff, sizeof( readBuff ) );
	    printf( "The recived string is : %s", readBuff );

	    //Writing to the target fileOpen
	    write( targetFile, readBuff, strlen( readBuff ) + 1 );
	} else {
	    // inside the parent process
	    close( fdone[0] );
	    // code to read from a text file

	    while( (readCounter = read( fileOpen, readBuff, sizeof( readBuff ) ) > 0 ) )  {
		write( fdone[1], readBuff, sizeof( readBuff ) );
	    }
	    close( fdone[1] );
	}
}
[/code]
Yay! Hope it gets someone in need.
