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
                        
                        Spacer(modifier=Modifier.height(20.dp))

                        // Garrafa de Água Visual
                        Box(
                            modifier=Modifier
                            .width(80.dp)
                            .height(160.dp)
                            .background(Color(0xFFF1F4F8),RoundedCornerShape(40.dp)),
                            contentAlignment=Alignment.BottomCenter
                        ){
                            Box(
                                modifier=Modifier
                                .fillMaxWidth
                                .fillMaxHeight((aguaConsumida/metaDiaria).coerceln(0f,1f))
                                .background(corAzulAgua,RoundedCornerShape(40.dp))
                            )
                        }
                        Spacer(modifier=Modifier.height(12.dp))
                        Text("${(aguaConsumida*1000).tolnt()}ml consumidos",fontSize=14.sp,color=Color.Gray)
                    }
                }
                Spacer(modifier=Modifier.height(24.dp))

                // Seção de Adicionar
                Text(
                    "Adicionar à meta",
                    fontWeight=FontWeight.Bold,
                    modifier=Modifier.align(Alignment.Start).padding(bottom=12.dp)
                )
                Row(modifier=Modifier.fillMaxWidth(),horizontalArrangement=Arrangement.spacedBy(12.dp)){
                    ItemAgua("Copo","250ml","💧",Modifier.weight(1f)){aguaConsumida+=0.25f}
                    ItemAgua("Suco","300ml","🥤",Modifier.weight(1f)){aguaConsumida+=0.30f}
                    ItemAgua("Chá","200ml","🍵",Modifier.weight(1f)){aguaConsumida+=0.20f}
                }
                Spacer(modifier=Modifier.height(30.dp))

                // Calculadora

                if(!mostrarCalculadora){
                    Button(
                        onClick={mostrarCalculadora=true},
                        modifier=Modifier.fillMaxWidth().height(56.dp),
                        colors=ButtonDefaults.buttonColors(containerColor=Color(0xFF5733FF)),
                        shape=RoundedCornerShape(12.dp)
                    ){
                        Icon(Icon.Default.Calculate,null)
                        Spacer(modifier=Modifier.width(8.dp))
                        Text("Calcular Meta por peso",fontWeight=FontWeight.Bold)
                    }
                } else{
                    Card(
                        modifier=Modifier.fillMaxWidth(),
                        shape=RoundedCornerShape(16.dp),
                        colors=CardDefaults.cardColors(containerColor=Color.White.copy(alpha=0.9f))
                    ){
                        Column(modifier=Modifier.padding(20.dp)){
                            Text("Calculadora Científica",fontWeight=FontWeight.Bold,color=Color(0xFF5733FF))
                            Spacer(modifier=Modifier.height(12.dp))

                            OutlinedTextField(
                                value=peso,
                                onVolueChange={peso=it},
                                label={Text("Seu peso atual(kg)")},
                                modifier=Modifier.fillMaxWidth(),
                                shape=RoundedCornerShape(12.dp)
                            )

                            Spacer(modifier=Modifier.height(16.dp))

                            Button(
                                onClick={
                                    val p=peso.toFloatOrNull()?:0f
                                    metaDiaria=(p*35)/1000
                                    mostrarCalculadora=false
                                },
                                modifier=Modifier.fillMaxWidth(),
                                colors=ButtonDefaults.buttonColors(containerColor=corAzulAgua)
                            ){
                                Text("Salvar Nova Meta")
                            }
                        }
                    }
                }
            }
        }
    }
}

// Componente Item Água 

@Composable
fun ItemAgua(nome:String,qtd:String,emoji:String,modifier:Modifier,onClick:()->Unit){
    Card(
        modifier=modifier.clickable{onClick()},
        shape=RoundedCornerShape(16.dp),
        colors=CardDefaults.cardColors(containerColor=Color.White),
        elevation=CardDefaults.cardElevation(2.dp)
    ){
        Column(
            modifier=Modifier.padding(16.dp).fillMaxWidth(),
            horizontalAlignment=Alignment.CenterHorizontally
        ){
            Text(emoji.fontSize=28.sp)
            Spacer(modifier=Modifier.height(4.dp))
            Text(nome,fontWeight=FontWeight.Bold,fontSize=14.sp)
            Text(qtd,color=Color.Gray,fontSize=12.sp)
        }
    }
}
@Preview(showSystemUi=true)
@Composable
fun PreviewHidratacao(){
    TelaHidratacao(onVoltar={})
}
