package com.example.sportgo

import androidx.compose.foundation.background
import androidx.compose.foundation.clickable
import androidx.compose.foundation.layout.*
import androidx.compose.foundation.rememberScrollState
import androidx.compose.foundation.shape.CircleShape
import androidx.compose.foundation.shape.RoundedCornerShape
import androidx.compose.foundation.verticalScroll
import androidx.compose.material.icons.Icons
import androidx.compose.material.icons.filled.*
import androidx.compose.material3.*
import androidx.compose.runtime.*
import androidx.compose.ui.Alignment
import androidx.compose.ui.Modifier
import androidx.compose.ui.graphics.Brush
import androidx.compose.ui.graphics.Color
import androidx.compose.ui.text.font.FontWeight
import androidx.compose.ui.tooling.preview.Preview
import androidx.compose.ui.unit.dp
import androidx.compose.ui.unit.sp

@OptIn(ExperimentalMaterial3Api::class)
@Composable
fun TelaHidratacao(
    onVoltar:()->Unit//Parâmetro adicionado para a navegação
){
    // Estados
    var metaDiaria by remember{mutableStateOf(2.5f)}
    var aguaConsumida by remember{mutableStateOf(0.95f)}

    // Estados para a Calculadora
    var peso by remember{mutableStateOf("")}
    var mostrarCalculadora by remember{mutableStateOf(false)}

    // Cores(Estética Clara do SportGo)
    val coresGradiente=listOf(Color(0xFFE0EAFC),Color(0xFFF7966B))
    val corAzulAgua=Color(0xFF2196F3)
    val corFundoCards=Color.White

    Scaffold(
        topBar={
            TopAppBar(
                title={Text("HydroTrack",fontWeight=FontWeight.Bold)},
                navigationICon={
                    IconButton(onClick=onVoltar){
                        Icon(Icons.Default.ArroBack,contentDescription="Voltar")
                    }
                },
                colors=TopappBarDefaults.topAppBarColors(
                    containerColor=Color.Transparent
                )
            )
        },
        containerColor=Color.Transparent//Permite que o Box com gradiente apareça
    ){paddingValues->
        Box(
            modifier=Modifier
                .fillMaxSize()
                .background(Brush.verticalGradient(coresGradiente))
                .padding(paddingValues)
        ){
            Column(
                modifier=Modifier
                    .fillMaxSize()
                    .verticalScroll(rememberScrollState())
                    .padding(20.dp),
                horizontalAlignment=Alignment.CenterHorizontally
            ){
                // Cabeçalho Interno
                Row(
                    modifier=Modifier.fillMaxWidth().
                    horizontalArrangement=Arrangement.SpaceBetween,
                    verticalAlignment=Alignment.CenterVertically
                ){
                    Column{
                        Text("Olá,Maria!", fontSize=28.sp,fontWeight=FontWeight.Bold)
                        Text("Mantenha-se hidratada hoje",color=Color.DarkGray,fontSize=14.sp)
                    }
                    IconButton(
                        onClick={},
                        modifier=Modifier.background(Color.White.copy(alpha=0.5f),CircleShape)
                    ){
                        Icon(Icons.Default.Notifications,contentDescription=null)
                    }
                }
                Spacer(modifier=Modifier.height(24.dp))
                // Card Principal:Proresso
                Card(
                    modifier=Modifier.fillMaxWidth(),
                    shape=RoundedCornerShape(24.dp),
                    colors=CardDefaults.cardColors(containerColor=corFundoCards),
                    elevation=CardDefaults.cardElevation(4.dp)
                ){
                    Column(
                        modifier=Modifier.padding(24.dp),
                        horizontalAlignment=Alignment.CenterHorizontally
                    ){
                        Text("Meta Diária", fontWeight=FontWeight.Bold,color=Color.Gray)
                        Text("${String.format("%.1f",metaDiaria)}L",fontSize=48.sp,fontWeight=FontWeight.Black,color=corAzulAgua)
                    }
                }
            }
        }
    }
}
