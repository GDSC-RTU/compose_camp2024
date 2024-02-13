@file:OptIn(ExperimentalMaterial3Api::class)

package com.example.worshop1

import android.annotation.SuppressLint
import android.os.Bundle
import androidx.activity.ComponentActivity
import androidx.activity.compose.setContent
import androidx.compose.foundation.Image
import androidx.compose.foundation.background
import androidx.compose.foundation.layout.Arrangement
import androidx.compose.foundation.layout.Box
import androidx.compose.foundation.layout.Column
import androidx.compose.foundation.layout.Row
import androidx.compose.foundation.layout.Spacer
import androidx.compose.foundation.layout.fillMaxSize
import androidx.compose.foundation.layout.fillMaxWidth
import androidx.compose.foundation.layout.height
import androidx.compose.foundation.layout.padding
import androidx.compose.foundation.layout.size
import androidx.compose.foundation.layout.width
import androidx.compose.foundation.lazy.LazyColumn
import androidx.compose.foundation.lazy.items
import androidx.compose.material.BottomAppBar
import androidx.compose.material.BottomNavigationItem
import androidx.compose.material.Icon
import androidx.compose.material.Scaffold
import androidx.compose.material.TopAppBar
import androidx.compose.material3.Card
import androidx.compose.material3.ExperimentalMaterial3Api
import androidx.compose.material3.IconButton
import androidx.compose.material3.MaterialTheme
import androidx.compose.material3.Surface
import androidx.compose.material3.Text
import androidx.compose.material3.TopAppBar
import androidx.compose.runtime.Composable
import androidx.compose.ui.Alignment
import androidx.compose.ui.Modifier
import androidx.compose.ui.graphics.Color
import androidx.compose.ui.layout.ContentScale
import androidx.compose.ui.res.painterResource
import androidx.compose.ui.res.stringResource
import androidx.compose.ui.text.TextStyle
import androidx.compose.ui.text.font.FontWeight
import androidx.compose.ui.text.style.TextAlign
import androidx.compose.ui.tooling.preview.Preview
import androidx.compose.ui.unit.dp
import androidx.compose.ui.unit.sp
import com.example.worshop1.ui.theme.Worshop1Theme

class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent {
            Worshop1Theme {
                // A surface container using the 'background' color from the theme
                Surface(
                    modifier = Modifier.fillMaxSize(),
                    color = MaterialTheme.colorScheme.background
                ) {
                    MyHomePage()
                }
            }
        }
    }
}

@SuppressLint("UnusedMaterialScaffoldPaddingParameter")
@Composable
fun MyHomePage() {
    Scaffold(
        topBar = { MyAppTopBar() },
        content = { PostFeed() },
        bottomBar = { MyAppBottomBar() }
    )
}

@Composable
fun MyAppBottomBar(){
    BottomAppBar(
        backgroundColor = Color.White, // Set the background color as needed
        elevation = 10.dp,
        modifier = Modifier.height(55.dp)
    ) {
        // Create BottomNavigationItems for each item in the bottom bar
        BottomNavigationItem(
            icon = {
                Icon(painter = painterResource(id = R.drawable.home_icon),
                    contentDescription = null,
                    modifier = Modifier
                        .size(22.dp)
                ) },
            label = null,
            selected = true, // Set to true for the selected item
            onClick = { /* Handle click */ },
        )
        BottomNavigationItem(
            icon = {
                Icon(painter = painterResource(id = R.drawable.search_icon),
                    contentDescription = null,
                    modifier = Modifier
                        .size(20.dp)
                ) },
            label = null,
            selected = false,
            onClick = { /* Handle click */ }
        )
        BottomNavigationItem(
            icon = {
                Icon(painter = painterResource(id = R.drawable.mail),
                    contentDescription = null,
                    modifier = Modifier
                        .size(20.dp)
                ) },
            label = null,
            selected = false,
            onClick = { /* Handle click */ }
        )
        BottomNavigationItem(
            icon = {
                Icon(painter = painterResource(id = R.drawable.notification),
                    contentDescription = null,
                    modifier = Modifier
                        .size(20.dp)
                ) },
            label = null,
            selected = false,
            onClick = { /* Handle click */ }
        )
    }
}

@Composable
fun MyAppTopBar() {
    TopAppBar(
        modifier = Modifier
            .fillMaxWidth()
            .height(60.dp),
        backgroundColor = Color.White,
        elevation = 2.dp
    ) {
        Row(
            horizontalArrangement = Arrangement.SpaceBetween,
            verticalAlignment = Alignment.CenterVertically,
            modifier = Modifier
                .fillMaxWidth()
                .padding(end = 5.dp)
        ) {
            Image(
                painter = painterResource(id = R.drawable.gdsc_logo),
                contentDescription = null,
                modifier = Modifier
                    .size(60.dp)
            )
            Image(
                painter = painterResource(id = R.drawable.profile2),
                contentDescription = null,
                modifier = Modifier
                    .size(40.dp)
            )
        }
    }
}


@Composable
fun PostFeed() {
    Column(
        modifier = Modifier.padding(bottom = 55.dp)
    ) {
        LazyColumn(
            modifier = Modifier
                .fillMaxSize()
                .background(Color.White)
        ) {
            items(Datasource().postList()) { post ->
                PostCard(post = post)
            }
        }
    }
}


@Composable
fun PostCard(post: Post) {
    Card(
        modifier = Modifier
            .fillMaxWidth()
            .padding(bottom = 2.dp)
            .background(Color.White),
//        elevation = 1.dp
    ){
        Box(
            modifier = Modifier
                .fillMaxSize()
                .background(Color.White)
        ) {
            Row(
                modifier = Modifier
                    .fillMaxSize()
                    .padding(10.dp)
                    .background(Color.White)
            ){
                Image(
                    painter = painterResource(id = post.imageResourceId),
                    contentDescription = null,
                    contentScale = ContentScale.Crop,
                    modifier = Modifier
                        .height(50.dp)
                        .width(50.dp)
                )
                Column(
                    modifier = Modifier.padding(start = 8.dp)
                ) {
                    Row {
                        Text(
                            text = post.name,
                            style = TextStyle(
                                fontWeight = FontWeight.Bold
                            ),
                            fontSize = 15.sp,
                            modifier = Modifier
                        )
                        Text(
                            text = " @" + post.username,
                            style = TextStyle(
                                fontWeight = FontWeight.Light
                            ),
                            fontSize = 15.sp,
                            color = Color(0xFF687684)
                        )
                        Text(
                            text = " " + post.time.toString() + "h",
                            style = TextStyle(
                                fontWeight = FontWeight.Light
                            ),
                            fontSize = 15.sp,
                            color = Color(0xFF687684)
                        )
                    }
                    //next code to written from here
                    //Adding the Space in between
                    Spacer(modifier = Modifier.height(4.dp))
                    //Body of the Card
                    Text(
                        text = stringResource(id = post.content),
                        style = TextStyle(
                            fontWeight = FontWeight.Medium
                        ),
                        fontSize = 15.sp
                    )
                    // Other tweet details can be added here
                    Row (
                        horizontalArrangement = Arrangement.SpaceBetween,
                        modifier = Modifier
                            .fillMaxWidth()
                            .padding(top = 10.dp, end = 50.dp)
                    ){
                        //next code to written from here
                        Row {
                            Image(
                                painter = painterResource(id = R.drawable.comment),
                                contentDescription = null,
                                modifier = Modifier
                                    .height(13.dp)
                                    .width(13.dp)
                                    .align(Alignment.CenterVertically)
                            )
                            Text(
                                text = post.comment.toString(),
                                fontSize = 12.sp,
                                style = TextStyle(
                                    fontWeight = FontWeight.Medium
                                ),
                                textAlign = TextAlign.Center,
                                color = Color(0xFF687684)
                            )
                        }
                        //next code to written from here
                        Row {
                            Image(
                                painter = painterResource(id = R.drawable.retweet),
                                contentDescription = null,
                                modifier = Modifier
                                    .height(13.dp)
                                    .width(13.dp)
                                    .align(Alignment.CenterVertically)
                            )
                            Text(
                                text = post.retweet.toString(),
                                fontSize = 12.sp,
                                style = TextStyle(
                                    fontWeight = FontWeight.Medium
                                ),
                                color = Color(0xFF687684)
                            )
                        }
                        Row {
                            Image(
                                painter = painterResource(id = R.drawable.like),
                                contentDescription = null,
                                modifier = Modifier
                                    .height(13.dp)
                                    .width(13.dp)
                                    .align(Alignment.CenterVertically)
                            )
                            Text(
                                text = post.likes.toString(),
                                fontSize = 12.sp,
                                style = TextStyle(
                                    fontWeight = FontWeight.Medium
                                ),
                                color = Color(0xFF687684)
                            )
                        }
                        //next code to written from here
                        Image(
                            painter = painterResource(id = R.drawable.upload),
                            contentDescription = null,
                            modifier = Modifier
                                .height(13.dp)
                                .width(13.dp)
                                .align(Alignment.CenterVertically)
                        )
                    }
                }
            }
        }
    }
}

@Preview(
    showSystemUi = true,
    showBackground = true
)
@Composable
fun PostCardPreview(){
    MyHomePage()
}



