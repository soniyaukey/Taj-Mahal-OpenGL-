#include <GL/gl.h>
#include <GL/glut.h>
#include <math.h>
#include <iostream>
#include <vector>
#include <windows.h>

///======================================///
///         Circle Function              ///
///======================================///

void drawCircle(float centerX, float centerY, float radius, int numSegments)
{
    const float angleIncrement = 2.0 * M_PI / numSegments;

    // Circle outline (black color, line width 2.0)
    glColor3f(0.0, 0.0, 0.0);
    glLineWidth(2.0);
    glBegin(GL_LINE_LOOP);
    for (int i = 0; i < numSegments; i++)
    {
        float theta = angleIncrement * float(i);
        float x = centerX + radius * cos(theta);
        float y = centerY + radius * sin(theta);
        glVertex2f(x, y);
    }
    glEnd();

    // Circle interior (light green color)
    glColor3f(0.945, 0.972, 0.914);
    glBegin(GL_POLYGON);
    for (int i = 0; i < numSegments; i++)
    {
        float theta = angleIncrement * float(i);
        float x = centerX + radius * cos(theta);
        float y = centerY + radius * sin(theta);
        glVertex2f(x, y);
    }
    glEnd();
}

///Cloud Circle

void Cloudscircle(GLfloat rx, GLfloat ry, GLfloat cx, GLfloat cy)
{
    glBegin(GL_POLYGON);
    glColor3f(1.0, 1.0, 1.0);
    glVertex2f(cx, cy);
    for (int i = 0; i <= 360; i++)
    {
        float angle = i * 3.1416 / 180;
        float x = rx * cos(angle);
        float y = ry * sin(angle);
        glVertex2f((x + cx), (y + cy));
    }
    glEnd();
}


///Small Cloud Function

float bx = 10; // Start the x-coordinate translation of the clouds at 10
void Smallclouds()
{
    glPushMatrix();
    glTranslatef(bx, 0, 0);

    // 1st small cloud
    Cloudscircle( 15,15 ,132 ,465 );
    Cloudscircle( 7,7 ,127 , 452);
    Cloudscircle( 10, 10,142 ,455 );
    Cloudscircle( 14,14 ,158 , 463);
    Cloudscircle( 14, 14, 143,477 );
    Cloudscircle( 11,11 ,122 ,477 );
    Cloudscircle( 15,15 ,114 ,464 );

// 2nd smalll cloud
    Cloudscircle(20,25, 360, 480);
    Cloudscircle(15, 15, 343, 480);
    Cloudscircle(13, 13, 338, 465);
    Cloudscircle(13, 15, 380, 482);
    Cloudscircle(10, 10, 380, 465);

    glPopMatrix();

    bx += 0.1; // Increase the translation by a larger value (adjust as needed)
    if (bx > 500)
        bx = -300; // Reset the x-coordinate translation when it reaches 500

    glutPostRedisplay();
}


///Large Cloud Function
float lx = 10;
void Largeclouds()
{
    glPushMatrix();
    glTranslatef(lx, 0, 0);

    // 1st Large cloud
    Cloudscircle(15,15, 187, 532);
    Cloudscircle(13, 13, 210, 531);
    Cloudscircle(13, 13, 222, 537);
    Cloudscircle(12, 12, 212, 550);
    Cloudscircle(16, 16, 194, 553);
    Cloudscircle(13, 13, 169, 547);
    Cloudscircle(11, 11, 166, 532);

    // 2nd Large cloud
    Cloudscircle( 14, 14,390 ,570 );
    Cloudscircle( 8, 8, 394, 560);
    Cloudscircle( 9,9 ,410 ,562 );
    Cloudscircle( 8, 8, 419,568 );
    Cloudscircle( 10, 10,410 ,577 );
    Cloudscircle( 9, 9, 393,582 );
    Cloudscircle( 8, 8,380 , 576);
    Cloudscircle( 9,9 ,369 ,568 );
    Cloudscircle( 9,9 ,380 ,560 );

    glPopMatrix();

    lx += 0.04; // Increase the translation by a larger value (adjust as needed)
    if (lx > 500)
        lx = -180; // Reset the x-coordinate translation

    glutPostRedisplay();
}


///======================================///
///           Sun Function              ///
///======================================///

float sunX = 75.0;
bool isDay = true;

void drawSun(float centerX, float centerY, float radius)
{
    // Set the sun color based on day/night transition
    if (isDay)
    {
        glColor3f(1.0, 0.9, 0.1); // Yellow color
    }
    else
    {
        glColor3f(1.0, 1.0, 1.0); // White color (moon)
    }

    // Draw the outer circle
    glBegin(GL_TRIANGLE_FAN);
    glVertex2f(centerX, centerY); // Center point

    int numSegments = 100;
    for (int i = 0; i <= numSegments; i++)
    {
        float theta = 2.0 * 3.14159 * float(i) / float(numSegments);
        float x = centerX + radius * cos(theta);
        float y = centerY + radius * sin(theta);
        glVertex2f(x, y);
    }
    glEnd();
}

///======================================///
///  BackGround Color Change Function    ///
///======================================///

void drawBackground()
{

    glBegin(GL_QUADS);
    if (isDay)
    {
        glColor3f(0.4, 0.6, 0.8); // Deep blue color
    }
    else
    {
        glColor3f(0.584, 0.792, 0.645); // Evening orange color

    }
    glVertex2f(0, 170);
    glVertex2f(600, 170);

    if (isDay)
    {
        glColor3f(0.984, 0.792, 0.545); // Evening orange color
    }
    else
    {
        glColor3f(0.05, 0.05, 0.15); // Dark blue color (night)

    }
    glVertex2f(600, 600);
    glVertex2f(0, 600);
    glEnd();
}

/// Day or Night Sun Move
void update(int value)
{
    // Update the sun position
    sunX += 0.2;
    // Wrap the sun position to create a continuous animation
    if (sunX > 625.0)
    {
        sunX = -25.0;
        isDay = !isDay; // Toggle day/night transition

        // Play sound effect based on day/night transition
        if (isDay)
        {
            PlaySound(TEXT("bird-2.wav"), NULL, SND_ASYNC);
        }
        else
        {
            PlaySound(TEXT("cricket-2.wav"), NULL, SND_ASYNC);
        }
    }

    // Set the next update interval
    glutTimerFunc(10, update, 0);

    // Redraw the scene
    glutPostRedisplay();
}



///======================================///
///           Rain Function              ///
///======================================///

struct Point
{
    float x, y;
    unsigned char r, g, b, a;
};

GLfloat position3 = 0.0f;
GLfloat speed3 = -0.8f;
std::vector<Point> points;

bool isRainActive = false;
bool isRainStarted = false;


void rain(int value)
{
    if (isRainActive)
    {
        if (position3 < -10.0)
            position3 = 5.0f;
        position3 += speed3;
        glutPostRedisplay();
    }
    glutTimerFunc(100, rain, 0);
}

void rainOn()
{
    glPushMatrix();

    glTranslatef(0.0f, position3, 0.0f);
    glColor3ub(255, 255, 255);
    glEnableClientState(GL_VERTEX_ARRAY);
    glEnableClientState(GL_COLOR_ARRAY);
    glVertexPointer(2, GL_FLOAT, sizeof(Point), &points[0].x);
    glColorPointer(4, GL_UNSIGNED_BYTE, sizeof(Point), &points[0].r);
    glPointSize(2.5);
    glDrawArrays(GL_POINTS, 0, points.size());
    glDisableClientState(GL_VERTEX_ARRAY);
    glDisableClientState(GL_COLOR_ARRAY);
    glPopMatrix();
}


///======================================///
///          Tree Function              ///
///======================================///
void drawLeftSideTrees() {

   /// Tree-01

    glBegin(GL_TRIANGLES);//4
    glColor3f(0.02, 0.416, 0.31);
    glVertex2f(35, 128);
    glVertex2f(65, 128);
    glVertex2f(50, 164);

    glBegin(GL_TRIANGLES);//3
    glColor3f(0.02, 0.416, 0.31);
    glVertex2f(32, 108);
    glVertex2f(68, 108);
    glVertex2f(50, 142);

    glEnd();
    glBegin(GL_TRIANGLES);//2
    glColor3f(0.02, 0.416, 0.31);
    glVertex2f(28, 85);
    glVertex2f(71, 85);
    glVertex2f(50, 125);
    glEnd();

    glBegin(GL_TRIANGLES);//1
    glColor3f(0.02, 0.416, 0.31);
    glVertex2f(25, 55);
    glVertex2f(75, 55);
    glVertex2f(50, 120);
    glEnd();

    //Body
    glColor3f(0.721, 0.537, 0.376);
    glBegin(GL_POLYGON);
    glVertex2f(44,36);
    glVertex2f(54,36);
    glVertex2f(54, 55);
    glVertex2f(44,55);
    glEnd();

    /// Tree-02

    glBegin(GL_TRIANGLES);//4
    glColor3f(0.02, 0.416, 0.31);
    glVertex2f(92, 142);
    glVertex2f(112, 142);
    glVertex2f(101, 159);

    glBegin(GL_TRIANGLES);//3
    glColor3f(0.02, 0.416, 0.31);
    glVertex2f(88, 126);
    glVertex2f(115, 126);
    glVertex2f(101, 149);

    glEnd();
    glBegin(GL_TRIANGLES);//2
    glColor3f(0.02, 0.416, 0.31);
    glVertex2f(85, 109);
    glVertex2f(118, 109);
    glVertex2f(101, 139);
    glEnd();

    glBegin(GL_TRIANGLES);//1
    glColor3f(0.02, 0.416, 0.31);
    glVertex2f(82, 86);
    glVertex2f(120, 86);
    glVertex2f(101, 120);
    glEnd();

    //Body
    glColor3f(0.721, 0.537, 0.376);
    glBegin(GL_POLYGON);
    glVertex2f(98,72);
    glVertex2f(105,72);
    glVertex2f(105, 86);
    glVertex2f(98,86);
    glEnd();


/// Left Tree-03

    glBegin(GL_TRIANGLES);//3
    glColor3f(0.02, 0.416, 0.31);
    glVertex2f(135, 145);
    glVertex2f(158, 145);
    glVertex2f(146, 160);
    glEnd();
    glBegin(GL_TRIANGLES);//2
    glColor3f(0.02, 0.416, 0.31);
    glVertex2f(132, 129);
    glVertex2f(161, 129);
    glVertex2f(146, 156);
    glEnd();

    glBegin(GL_TRIANGLES);//1
    glColor3f(0.02, 0.416, 0.31);
    glVertex2f(130, 109);
    glVertex2f(163,109);
    glVertex2f(146, 143);
    glEnd();

    //Body
    glColor3f(0.721, 0.537, 0.376);
    glBegin(GL_POLYGON);
    glVertex2f(144,97);
    glVertex2f(150,97);
    glVertex2f(150, 109);
    glVertex2f(144,109);
    glEnd();

    /// Left Tree-04

    glBegin(GL_TRIANGLES);//3
    glColor3f(0.02, 0.416, 0.31);
    glVertex2f(166, 144);
    glVertex2f(181, 144);
    glVertex2f(173, 158);
    glEnd();
    glBegin(GL_TRIANGLES);//2
    glColor3f(0.02, 0.416, 0.31);
    glVertex2f(164, 135);
    glVertex2f(183, 135);
    glVertex2f(173, 152);
    glEnd();

    glBegin(GL_TRIANGLES);//1
    glColor3f(0.02, 0.416, 0.31);
    glVertex2f(163, 122);
    glVertex2f(183, 122);
    glVertex2f(173, 142);
    glEnd();

    //Body
    glColor3f(0.721, 0.537, 0.376);
    glBegin(GL_POLYGON);
    glVertex2f(172,113);
    glVertex2f(175.5 ,113);
    glVertex2f(175.5, 122);
    glVertex2f(172 , 122);
    glEnd();

}
void drawRightSideTrees() {


///Tree-01
    glBegin(GL_TRIANGLES); // 4
    glColor3f(0.02, 0.416, 0.31);
    glVertex2f(535, 128);
    glVertex2f(565, 128);
    glVertex2f(550, 164);

    glBegin(GL_TRIANGLES); // 3
    glColor3f(0.02, 0.416, 0.31);
    glVertex2f(532, 108);
    glVertex2f(568, 108);
    glVertex2f(550, 142);

    glEnd();
    glBegin(GL_TRIANGLES); // 2
    glColor3f(0.02, 0.416, 0.31);
    glVertex2f(528, 85);
    glVertex2f(571, 85);
    glVertex2f(550, 125);
    glEnd();

    glBegin(GL_TRIANGLES); // 1
    glColor3f(0.02, 0.416, 0.31);
    glVertex2f(525, 55);
    glVertex2f(575, 55);
    glVertex2f(550, 120);
    glEnd();

// Body
    glColor3f(0.721, 0.537, 0.376);
    glBegin(GL_POLYGON);
    glVertex2f(544, 36);
    glVertex2f(554, 36);
    glVertex2f(554, 55);
    glVertex2f(544, 55);
    glEnd();

/// Tree-02 (Right Side)

    glBegin(GL_TRIANGLES); // 4
    glColor3f(0.02, 0.416, 0.31);
    glVertex2f(483, 142);
    glVertex2f(507, 142);
    glVertex2f(495, 159);
    glEnd();

    glBegin(GL_TRIANGLES); // 3
    glColor3f(0.02, 0.416, 0.31);
    glVertex2f(480, 126);
    glVertex2f(510, 126);
    glVertex2f(495, 149);
    glEnd();

    glBegin(GL_TRIANGLES); // 2
    glColor3f(0.02, 0.416, 0.31);
    glVertex2f(479, 109);
    glVertex2f(512, 109);
    glVertex2f(495, 139);
    glEnd();

    glBegin(GL_TRIANGLES); // 1
    glColor3f(0.02, 0.416, 0.31);
    glVertex2f(476, 86);
    glVertex2f(514, 86);
    glVertex2f(495, 120);
    glEnd();

// Body
    glColor3f(0.721, 0.537, 0.376);
    glBegin(GL_POLYGON);
    glVertex2f(490, 72);
    glVertex2f(497, 72);
    glVertex2f(497, 86);
    glVertex2f(490, 86);
    glEnd();

/// Tree 3

    glBegin(GL_TRIANGLES); // 3
    glColor3f(0.02, 0.416, 0.31);
    glVertex2f(442, 145);
    glVertex2f(465, 145);
    glVertex2f(453, 160);
    glEnd();

    glBegin(GL_TRIANGLES); // 2
    glColor3f(0.02, 0.416, 0.31);
    glVertex2f(437, 129);
    glVertex2f(466, 129);
    glVertex2f(453, 156);
    glEnd();

    glBegin(GL_TRIANGLES); // 1
    glColor3f(0.02, 0.416, 0.31);
    glVertex2f(435, 109);
    glVertex2f(468, 109);
    glVertex2f(453, 143);
    glEnd();

// Body
    glColor3f(0.721, 0.537, 0.376);
    glBegin(GL_POLYGON);
    glVertex2f(449, 97);
    glVertex2f(455, 97);
    glVertex2f(455, 109);
    glVertex2f(449, 109);
    glEnd();

/// Right Tree-04

    glBegin(GL_TRIANGLES); // 3
    glColor3f(0.02, 0.416, 0.31);
    glVertex2f(418, 144);
    glVertex2f(435, 144);
    glVertex2f(426, 158);
    glEnd();

    glBegin(GL_TRIANGLES); // 2
    glColor3f(0.02, 0.416, 0.31);
    glVertex2f(417, 135);
    glVertex2f(436, 135);
    glVertex2f(426, 152);
    glEnd();

    glBegin(GL_TRIANGLES); // 1
    glColor3f(0.02, 0.416, 0.31);
    glVertex2f(417, 122);
    glVertex2f(437, 122);
    glVertex2f(427, 142);
    glEnd();

// Body
    glColor3f(0.721, 0.537, 0.376);
    glBegin(GL_POLYGON);
    glVertex2f(426, 113);
    glVertex2f(429.5, 113);
    glVertex2f(429.5, 122);
    glVertex2f(426, 122);
    glEnd();
}

/// Tree Function End here


/// ====================== ///
/// Main Display Function  ///


void display(void)
{

    glClear (GL_COLOR_BUFFER_BIT);


//Sun
    drawBackground();
    drawSun(sunX, 535.0, 26.0);

//Cloud
    Smallclouds();
    Largeclouds();


///.......................
///Lower Slide of TajMahal
///........................

    glColor3f(0.772, 0.882, 0.647);
    glBegin(GL_POLYGON);
    glVertex2f(0,0);
    glVertex2f(0,170);
    glVertex2f(600, 170);
    glVertex2f(600,0 );
    glEnd();

//Tree
drawLeftSideTrees();
drawRightSideTrees();




///======================================///
///               Lower Base             ///
///======================================///

    glColor3f(0.945, 0.972, 0.914);
    glBegin(GL_POLYGON);
    glVertex2f(232,170);
    glVertex2f(365,170);
    glVertex2f(416, 156);
    glVertex2f(185,156);
    glEnd();
    // Black Line
    glLineWidth(1.0);
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glVertex2f(232, 170);
    glVertex2f(365, 170);
    glVertex2f(416, 156);
    glVertex2f(185, 156);
    glEnd();

    glColor3f(0.945, 0.972, 0.914);
    glBegin(GL_POLYGON);
    glVertex2f(185,156);
    glVertex2f(416, 156);
    glVertex2f(417, 140);
    glVertex2f(185,140);
    glEnd();

    // Black Line
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glVertex2f(185, 156);
    glVertex2f(416, 156);
    glVertex2f(417, 140);
    glVertex2f(185, 140);
    glEnd();

///Left Side Road
    glColor3f(0.984, 0.914, 0.905);
    glBegin(GL_POLYGON);
    glVertex2f(220,140);
    glVertex2f(248, 140);
    glVertex2f(100, 0);
    glVertex2f(20,0);
    glEnd();

    // Black Line
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glVertex2f(220, 140);
    glVertex2f(248, 140);
    glVertex2f(100, 0);
    glVertex2f(20, 0);
    glEnd();

///Right Side Road
    glColor3f(0.984, 0.914, 0.905);
    glBegin(GL_POLYGON);
    glVertex2f(354,140);
    glVertex2f(380, 140);
    glVertex2f(582, 0);
    glVertex2f(500,0);
    glEnd();
    // Black Line
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glVertex2f(354,140);
    glVertex2f(380, 140);
    glVertex2f(582, 0);
    glVertex2f(500,0);
    glEnd();

///Water
    glColor3f(0.529, 0.808, 0.922);
    glBegin(GL_POLYGON);
    glVertex2f(248, 140);
    glVertex2f(354,140);
    glVertex2f(500, 0);
    glVertex2f(100,0);
    glEnd();


    // Black Line
    glLineWidth(1.3);
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glVertex2f(248, 140);
    glVertex2f(354, 140);
    glVertex2f(500, 0);
    glVertex2f(100, 0);
    glEnd();


///Base
    glColor3f(0.973, 0.957, 0.902);
    glBegin(GL_POLYGON);
    glVertex2f(60, 198);
    glVertex2f(60,170);
    glVertex2f(541, 170);
    glVertex2f(541,198);
    glEnd();

    // Black Line
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glVertex2f(60, 198);
    glVertex2f(60, 170);
    glVertex2f(541, 170);
    glVertex2f(541, 198);
    glEnd();

///base devide left to right
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINES);
    glVertex2f(114, 198);
    glVertex2f(114, 170);

    glVertex2f(249, 198);
    glVertex2f(249, 170);

    glVertex2f(353, 198);
    glVertex2f(353, 170);

    glVertex2f(488, 198);
    glVertex2f(488, 170);

    glEnd();

///Base Shape left to right
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);//1
    glVertex2f(116, 170);
    glVertex2f(116, 184);
    glVertex2f(123, 193);
    glVertex2f(130, 184);
    glVertex2f(130, 170);
    glEnd();

    glColor3f(0.0, 0.0, 0.0);//2
    glBegin(GL_LINE_LOOP);
    glVertex2f(136, 170);
    glVertex2f(136, 184);
    glVertex2f(142.5, 193);
    glVertex2f(149, 184);
    glVertex2f(149, 170);
    glEnd();

    glColor3f(0.0, 0.0, 0.0);//3
    glBegin(GL_LINE_LOOP);
    glVertex2f(155, 170);
    glVertex2f(155, 184);
    glVertex2f(162, 193);
    glVertex2f(169, 184);
    glVertex2f(169, 170);
    glEnd();

    glColor3f(0.0, 0.0, 0.0);//4
    glBegin(GL_LINE_LOOP);
    glVertex2f(174, 170);
    glVertex2f(174, 184);
    glVertex2f(181.5, 193);
    glVertex2f(188, 184);
    glVertex2f(188, 170);
    glEnd();
    glColor3f(0.0, 0.0, 0.0);//5
    glBegin(GL_LINE_LOOP);
    glVertex2f(194, 170);
    glVertex2f(194, 184);
    glVertex2f(201, 193);
    glVertex2f(207, 184);
    glVertex2f(207, 170);
    glEnd();
    glColor3f(0.0, 0.0, 0.0);//6
    glBegin(GL_LINE_LOOP);
    glVertex2f(213, 170);
    glVertex2f(213, 184);
    glVertex2f(220, 193);
    glVertex2f(227, 184);
    glVertex2f(227, 170);
    glEnd();
    glColor3f(0.0, 0.0, 0.0);//7
    glBegin(GL_LINE_LOOP);
    glVertex2f(232, 170);
    glVertex2f(232, 184);
    glVertex2f(239, 193);
    glVertex2f(246, 184);
    glVertex2f(246, 170);
    glEnd();

    glColor3f(0.0, 0.0, 0.0);//8
    glBegin(GL_LINE_LOOP);
    glVertex2f(253, 170);
    glVertex2f(253, 184);
    glVertex2f(260, 193);
    glVertex2f(267, 184);
    glVertex2f(267, 170);
    glEnd();

    glColor3f(0.0, 0.0, 0.0);//9
    glBegin(GL_LINE_LOOP);
    glVertex2f(273, 170);
    glVertex2f(273, 184);
    glVertex2f(280, 193);
    glVertex2f(288, 184);
    glVertex2f(288, 170);
    glEnd();

    glColor3f(0.0, 0.0, 0.0);//10
    glBegin(GL_LINE_LOOP);
    glVertex2f(293, 170);
    glVertex2f(293, 184);
    glVertex2f(300, 193);
    glVertex2f(308, 184);
    glVertex2f(308, 170);
    glEnd();

    glColor3f(0.0, 0.0, 0.0);//11
    glBegin(GL_LINE_LOOP);
    glVertex2f(314, 170);
    glVertex2f(314, 184);
    glVertex2f(322, 193);
    glVertex2f(329, 184);
    glVertex2f(329, 170);
    glEnd();
    glColor3f(0.0, 0.0, 0.0);//12
    glBegin(GL_LINE_LOOP);
    glVertex2f(334, 170);
    glVertex2f(334, 184);
    glVertex2f(341, 193);
    glVertex2f(348, 184);
    glVertex2f(348, 170);
    glEnd();

    glColor3f(0.0, 0.0, 0.0);//13
    glBegin(GL_LINE_LOOP);
    glVertex2f(356, 170);
    glVertex2f(356, 184);
    glVertex2f(363, 193);
    glVertex2f(370, 184);
    glVertex2f(370, 170);
    glEnd();

    glColor3f(0.0, 0.0, 0.0);//14
    glBegin(GL_LINE_LOOP);
    glVertex2f(375, 170);
    glVertex2f(375, 184);
    glVertex2f(382, 193);
    glVertex2f(389, 184);
    glVertex2f(389, 170);
    glEnd();
    glColor3f(0.0, 0.0, 0.0);//15
    glBegin(GL_LINE_LOOP);
    glVertex2f(394, 170);
    glVertex2f(394, 184);
    glVertex2f(401, 193);
    glVertex2f(408, 184);
    glVertex2f(408, 170);
    glEnd();

    glColor3f(0.0, 0.0, 0.0);//16
    glBegin(GL_LINE_LOOP);
    glVertex2f(413, 170);
    glVertex2f(413, 184);
    glVertex2f(420, 193);
    glVertex2f(427, 184);
    glVertex2f(427, 170);
    glEnd();

    glColor3f(0.0, 0.0, 0.0);//17
    glBegin(GL_LINE_LOOP);
    glVertex2f(433, 170);
    glVertex2f(433, 184);
    glVertex2f(440, 193);
    glVertex2f(447, 184);
    glVertex2f(447, 170);
    glEnd();

    glColor3f(0.0, 0.0, 0.0);//18
    glBegin(GL_LINE_LOOP);
    glVertex2f(452, 170);
    glVertex2f(452, 184);
    glVertex2f(459, 193);
    glVertex2f(466, 184);
    glVertex2f(466, 170);
    glEnd();

    glColor3f(0.0, 0.0, 0.0);//19
    glBegin(GL_LINE_LOOP);
    glVertex2f(472, 170);
    glVertex2f(472, 184);
    glVertex2f(479, 193);
    glVertex2f(485, 184);
    glVertex2f(485, 170);
    glEnd();

///===================================///
///                Minar              ///
///===================================///


///left font Minar
    glColor3f(0.945, 0.972, 0.914);
    glBegin(GL_POLYGON);
    glVertex2f(66, 198); //Below Part
    glVertex2f(109,198);
    glVertex2f(106, 250);
    glVertex2f(70,250);
    glEnd();
    // Black Line
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glVertex2f(66, 198);
    glVertex2f(109, 198);
    glVertex2f(106, 250);
    glVertex2f(70, 250);
    glEnd();

    glColor3f(0.945, 0.972, 0.914);
    glBegin(GL_POLYGON);
    glVertex2f(70, 250); //Bleow thick 1st part
    glVertex2f(106, 250);
    glVertex2f(110,253);
    glVertex2f(110,259);
    glVertex2f(66,259);
    glVertex2f(66,253);
    glEnd();

    // Black Line
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glVertex2f(70, 250);
    glVertex2f(106, 250);
    glVertex2f(110,253);
    glVertex2f(110,259);
    glVertex2f(66,259);
    glVertex2f(66,253);
    glEnd();

    glColor3f(0.0, 0.0, 0.0); //Single Line
    glBegin(GL_LINES);
    glVertex2f(66, 253);
    glVertex2f(110, 253);
    glEnd();



    //Middle Part
    glColor3f(0.945, 0.972, 0.914);
    glBegin(GL_POLYGON);
    glVertex2f(70, 259); //Middle Part
    glVertex2f(105,259);
    glVertex2f(102, 312);
    glVertex2f(74,312);
    glEnd();
    // Black Line
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glVertex2f(70, 259); //Middle Side
    glVertex2f(105,259);
    glVertex2f(102, 312);
    glVertex2f(74,312);
    glEnd();

    //Middle thik part
    glColor3f(0.945, 0.972, 0.914);
    glBegin(GL_POLYGON); // Middle thik Part
    glVertex2f(74, 312);
    glVertex2f(70, 315);
    glVertex2f(70,320);
    glVertex2f(106,320);
    glVertex2f(106,315);
    glVertex2f(102,312);
    glEnd();

    // Black Line
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glVertex2f(74, 312);
    glVertex2f(70, 315);
    glVertex2f(70,320);
    glVertex2f(106,320);
    glVertex2f(106,315);
    glVertex2f(102,312);
    glEnd();

    glColor3f(0.0, 0.0, 0.0); //Single Line
    glBegin(GL_LINES);
    glVertex2f(106, 315);
    glVertex2f(70, 315);
    glEnd();

//Font-Minar_Upper Part
    glColor3f(0.945, 0.972, 0.914);
    glBegin(GL_POLYGON);
    glVertex2f(75, 320);
    glVertex2f(100,320);
    glVertex2f(97, 374);
    glVertex2f(79,374);
    glEnd();
    // Black Line
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glVertex2f(75, 320);
    glVertex2f(100,320);
    glVertex2f(97, 374);
    glVertex2f(79,374);
    glEnd();

//Left Font-Minar_Upper
// thik part
    glColor3f(0.945, 0.972, 0.914);
    glBegin(GL_POLYGON);
    glVertex2f(79, 374);
    glVertex2f(71, 379);
    glVertex2f(77,384);
    glVertex2f(100,384);
    glVertex2f(104,379);
    glVertex2f(98,374);
    glEnd();

    // Black Line
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glVertex2f(79, 374);
    glVertex2f(71, 379);
    glVertex2f(77,384);
    glVertex2f(100,384);
    glVertex2f(105,379);
    glVertex2f(98,374);
    glEnd();

    glColor3f(0.0, 0.0, 0.0); //Single Line
    glBegin(GL_LINES);
    glVertex2f(71, 379);
    glVertex2f(105,379);
    glEnd();

//Left font minar Dome
    glLineWidth(2.0);
    glColor3f(0.0, 0.0, 0.0); //Single Line
    glBegin(GL_LINES);
    glVertex2f(88.4, 411);
    glVertex2f(88.4, 421);
    glEnd();

    // Circle Outline
    glLineWidth(2.0);
    glColor3f(0.0, 0.0, 0.0); // Black color
    glBegin(GL_LINE_LOOP);
    for (int i = 0; i < 360; i++)
    {
        float angle = i * 3.14159 / 180;
        float x = 88.8 + 11 * cos(angle);
        float y = 399.4 + 11 * sin(angle);
        glVertex2f(x, y);
    }
    glEnd();

    // Circle Fill
    glColor3f(0.945, 0.972, 0.914);
    glBegin(GL_POLYGON);
    for (int i = 0; i < 360; i++)
    {
        float angle = i * 3.14159 / 180;
        float x = 88.8 + 11 * cos(angle);
        float y = 399.4 + 11 * sin(angle);
        glVertex2f(x, y);
    }
    glEnd();

//  Left_Font-Minar
//  Squar-part
    glColor3f(0.945, 0.972, 0.914);
    glBegin(GL_POLYGON);
    glVertex2f(77, 384);
    glVertex2f(77,397);
    glVertex2f(100, 397);
    glVertex2f(100,384);
    glEnd();
    // Black Line
    glLineWidth(1.0);
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glVertex2f(77, 384);
    glVertex2f(77,397);
    glVertex2f(100, 397);
    glVertex2f(100,384);
    glEnd();

//Upper_Squar-part
//Within 3 part
    glColor3f(0.733, 0.871, 0.984);
    glBegin(GL_POLYGON); //1
    glVertex2f(79, 384);
    glVertex2f(79, 391);
    glVertex2f(80.6,395);
    glVertex2f(82.5,391);
    glVertex2f(82.5,384);
    glEnd();

    // Black Line
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);//1
    glVertex2f(79, 384);
    glVertex2f(79, 391);
    glVertex2f(80.6,395);
    glVertex2f(82.5,391);
    glVertex2f(82.5,384);
    glEnd();

    glColor3f(0.733, 0.871, 0.984);
    glBegin(GL_POLYGON); //2
    glVertex2f(86, 384);
    glVertex2f(86, 393);
    glVertex2f(88.5,396);
    glVertex2f(91,393);
    glVertex2f(91,384);
    glEnd();

    // Black Line
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glVertex2f(86, 384);//2
    glVertex2f(86, 393);
    glVertex2f(88.5,396);
    glVertex2f(91,393);
    glVertex2f(91,384);
    glEnd();

    glColor3f(0.733, 0.871, 0.984);
    glBegin(GL_POLYGON); //3
    glVertex2f(94, 384);
    glVertex2f(94, 391);
    glVertex2f(96,395);
    glVertex2f(98,391);
    glVertex2f(98,384);
    glEnd();

    // Black Line
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);//3
    glVertex2f(94, 384);
    glVertex2f(94, 391);
    glVertex2f(96,395);
    glVertex2f(98,391);
    glVertex2f(98,384);
    glEnd();


///............................
///      Left Back Minar     //
///............................
    glColor3f(0.945, 0.972, 0.914);
    glBegin(GL_POLYGON);
    glVertex2f(118, 198); //Below Part
    glVertex2f(151,198);
    glVertex2f(148, 235);
    glVertex2f(121,235);
    glEnd();
    // Black Line
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glVertex2f(118, 198); //Below Part
    glVertex2f(151,198);
    glVertex2f(148, 235);
    glVertex2f(121,235);
    glEnd();

    glColor3f(0.945, 0.972, 0.914);
    glBegin(GL_POLYGON);
    glVertex2f(121, 235); //Bleow thick 1st part
    glVertex2f(117, 237);
    glVertex2f(117,242);
    glVertex2f(152,242);
    glVertex2f(152,237);
    glVertex2f(148,235);
    glEnd();

    // Black Line
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glVertex2f(121, 235); //Bleow thick 1st part
    glVertex2f(117, 237);
    glVertex2f(117,242);
    glVertex2f(152,242);
    glVertex2f(152,237);
    glVertex2f(148,235);
    glEnd();

    glColor3f(0.0, 0.0, 0.0); //Single Line
    glBegin(GL_LINES);
    glVertex2f(152,237);
    glVertex2f(117, 237);
    glEnd();


//Middle Part
    glColor3f(0.945, 0.972, 0.914);
    glBegin(GL_POLYGON);
    glVertex2f(122, 242); //Middle Part
    glVertex2f(124,282);
    glVertex2f(146, 282);
    glVertex2f(148,242);
    glEnd();
    // Black Line
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glVertex2f(122, 242); //Middle Part
    glVertex2f(124,282);
    glVertex2f(146, 282);
    glVertex2f(148,242);
    glEnd();

    //Middle thik part
    glColor3f(0.945, 0.972, 0.914);
    glBegin(GL_POLYGON); // Middle thik Part
    glVertex2f(124, 282);
    glVertex2f(121, 285);
    glVertex2f(121,289);
    glVertex2f(149,289);
    glVertex2f(149,285);
    glVertex2f(146,282);
    glEnd();

    // Black Line
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glVertex2f(124, 282);
    glVertex2f(121, 285);
    glVertex2f(121,289);
    glVertex2f(149,289);
    glVertex2f(149,285);
    glVertex2f(146,282);
    glEnd();

    glColor3f(0.0, 0.0, 0.0); //Single Line
    glBegin(GL_LINES);
    glVertex2f(149,285);
    glVertex2f(121, 285);
    glEnd();



//Left Back-Minar_Upper Part
    glColor3f(0.945, 0.972, 0.914);
    glBegin(GL_POLYGON);
    glVertex2f(125, 289);
    glVertex2f(127,329);
    glVertex2f(142, 329);
    glVertex2f(145,289);
    glEnd();
    // Black Line
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glVertex2f(125, 289);
    glVertex2f(127,329);
    glVertex2f(142, 329);
    glVertex2f(145,289);
    glEnd();

//Left Back-Minar_Upper
// thik part
    glColor3f(0.945, 0.972, 0.914);
    glBegin(GL_POLYGON);
    glVertex2f(127,329);
    glVertex2f(122, 333);
    glVertex2f(127,336);
    glVertex2f(143,336);
    glVertex2f(147,333);
    glVertex2f(142, 329);
    glEnd();

    // Black Line
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glVertex2f(127,329);
    glVertex2f(122, 333);
    glVertex2f(127,336);
    glVertex2f(143,336);
    glVertex2f(147,333);
    glVertex2f(142, 329);
    glEnd();

//............................

//Left Back minar Dome
    glLineWidth(1.5);
    glColor3f(0.0, 0.0, 0.0); //Single Line
    glBegin(GL_LINES);
    glVertex2f(134.9, 354);
    glVertex2f(134.9, 361);
    glEnd();

    // Circle Outline
    glLineWidth(2.0);
    glColor3f(0.0, 0.0, 0.0); // Black color
    glBegin(GL_LINE_LOOP);
    for (int i = 0; i < 360; i++)
    {
        float angle = i * 3.14159 / 180;
        float x = 134.9 + 8 * cos(angle);
        float y = 346 + 8 * sin(angle);
        glVertex2f(x, y);
    }
    glEnd();

    // Circle Fill
    glColor3f(0.945, 0.972, 0.914);
    glBegin(GL_POLYGON);
    for (int i = 0; i < 360; i++)
    {
        float angle = i * 3.14159 / 180;
        float x = 134.9 + 8 * cos(angle);
        float y = 346 + 8 * sin(angle);
        glVertex2f(x, y);
    }
    glEnd();

//............................

//  Left_Back-Minar
//  Squar-part
    glColor3f(0.945, 0.972, 0.914);
    glBegin(GL_POLYGON);
    glVertex2f(127,336);
    glVertex2f(127,346);
    glVertex2f(143, 346);
    glVertex2f(143,336);
    glEnd();
    // Black Line
    glLineWidth(1.0);
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glVertex2f(127,336);
    glVertex2f(127,346);
    glVertex2f(143, 346);
    glVertex2f(143,336);
    glEnd();

//Upper_Squar-part
//Within 3 part
    glColor3f(0.733, 0.871, 0.984);
    glBegin(GL_POLYGON); //1
    glVertex2f(129, 336);
    glVertex2f(129, 344);
    glVertex2f(131,344);
    glVertex2f(131,336);

    glEnd();

    // Black Line
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);//1
    glVertex2f(129, 336);
    glVertex2f(129, 344);
    glVertex2f(131,344);
    glVertex2f(131,336);
    glEnd();

    glColor3f(0.733, 0.871, 0.984);
    glBegin(GL_POLYGON); //2
    glVertex2f(133, 336);
    glVertex2f(133, 344);
    glVertex2f(137,344);
    glVertex2f(137,336);

    glEnd();

    // Black Line
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);//2
    glVertex2f(133, 336);
    glVertex2f(133, 344);
    glVertex2f(137,344);
    glVertex2f(137,336);
    glEnd();

    glColor3f(0.733, 0.871, 0.984);
    glBegin(GL_POLYGON); //2
    glVertex2f(139, 336);
    glVertex2f(139, 344);
    glVertex2f(142,344);
    glVertex2f(142,336);

    glEnd();

    // Black Line
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);//3
    glVertex2f(139, 336);
    glVertex2f(139, 344);
    glVertex2f(142,344);
    glVertex2f(142,336);
    glEnd();


///............................
///       Right Font Minar
///............................

//left font Minar
    glColor3f(0.945, 0.972, 0.914);
    glBegin(GL_POLYGON);
    glVertex2f(492, 198); //Below Part
    glVertex2f(535,198);
    glVertex2f(532, 250);
    glVertex2f(496,250);
    glEnd();
    // Black Line
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glVertex2f(492, 198); //Below Part
    glVertex2f(535,198);
    glVertex2f(532, 250);
    glVertex2f(496,250);
    glEnd();
    glEnd();

    glColor3f(0.945, 0.972, 0.914);
    glBegin(GL_POLYGON);
    glVertex2f(496, 250); //Bleow thick 1st part
    glVertex2f(532, 250);
    glVertex2f(536,253);
    glVertex2f(536,259);
    glVertex2f(492,259);
    glVertex2f(492,253);
    glEnd();

    // Black Line
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glVertex2f(496, 250); //Bleow thick 1st part
    glVertex2f(532, 250);
    glVertex2f(536,253);
    glVertex2f(536,259);
    glVertex2f(492,259);
    glVertex2f(492,253);
    glEnd();

    glColor3f(0.0, 0.0, 0.0); //Single Line
    glBegin(GL_LINES);
    glVertex2f(492, 253);
    glVertex2f(536, 253);
    glEnd();
//...........................
//Middle Part
    glColor3f(0.945, 0.972, 0.914);
    glBegin(GL_POLYGON);
    glVertex2f(497, 259); //Middle Part
    glVertex2f(530,259);
    glVertex2f(527, 312);
    glVertex2f(500,312);
    glEnd();
    // Black Line
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glVertex2f(497, 259); //Middle Part
    glVertex2f(530,259);
    glVertex2f(527, 312);
    glVertex2f(500,312);
    glEnd();

    //Middle thik part
    glColor3f(0.945, 0.972, 0.914);
    glBegin(GL_POLYGON); // Middle thik Part
    glVertex2f(500, 312);
    glVertex2f(495, 315);
    glVertex2f(495,320);
    glVertex2f(533,320);
    glVertex2f(533,315);
    glVertex2f(527,312);
    glEnd();

    // Black Line
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glVertex2f(500, 312);
    glVertex2f(495, 315);
    glVertex2f(495,320);
    glVertex2f(533,320);
    glVertex2f(533,315);
    glVertex2f(527,312);
    glEnd();

    glColor3f(0.0, 0.0, 0.0); //Single Line
    glBegin(GL_LINES);
    glVertex2f(533, 315);
    glVertex2f(495, 315);
    glEnd();

//Right Font-Minar_Upper Part
    glColor3f(0.945, 0.972, 0.914);
    glBegin(GL_POLYGON);
    glVertex2f(500, 320);
    glVertex2f(527,320);
    glVertex2f(524, 374);
    glVertex2f(504,374);
    glEnd();
    // Black Line
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glVertex2f(500, 320);
    glVertex2f(527,320);
    glVertex2f(524, 374);
    glVertex2f(504,374);
    glEnd();
    glEnd();

//Right Font-Minar_Upper
// thik part
    glColor3f(0.945, 0.972, 0.914);
    glBegin(GL_POLYGON);
    glVertex2f(504, 374);
    glVertex2f(496, 379);
    glVertex2f(503,384);
    glVertex2f(525,384);
    glVertex2f(531,379);
    glVertex2f(524,374);
    glEnd();

    // Black Line
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glVertex2f(504, 374);
    glVertex2f(496, 379);
    glVertex2f(503,384);
    glVertex2f(525,384);
    glVertex2f(531,379);
    glVertex2f(524,374);
    glEnd();

    glColor3f(0.0, 0.0, 0.0); //Single Line
    glBegin(GL_LINES);
    glVertex2f(531, 379);
    glVertex2f(496,379);
    glEnd();
//...................


//Right font minar Dome
    glLineWidth(2.0);
    glColor3f(0.0, 0.0, 0.0); //Single Line
    glBegin(GL_LINES);
    glVertex2f(514.4, 411);
    glVertex2f(514.4, 421);
    glEnd();

    // Circle Outline
    glLineWidth(2.0);
    glColor3f(0.0, 0.0, 0.0); // Black color
    glBegin(GL_LINE_LOOP);
    for (int i = 0; i < 360; i++)
    {
        float angle = i * 3.14159 / 180;
        float x = 514.4 + 11 * cos(angle);
        float y = 399.4 + 11 * sin(angle);
        glVertex2f(x, y);
    }
    glEnd();

    // Circle Fill
    glColor3f(0.945, 0.972, 0.914);
    glBegin(GL_POLYGON);
    for (int i = 0; i < 360; i++)
    {
        float angle = i * 3.14159 / 180;
        float x = 514.4 + 11 * cos(angle);
        float y = 399.4 + 11 * sin(angle);
        glVertex2f(x, y);
    }
    glEnd();

//  Left_Font-Minar
//  Squar-part
    glColor3f(0.945, 0.972, 0.914);
    glBegin(GL_POLYGON);
    glVertex2f(503, 384);
    glVertex2f(503,397);
    glVertex2f(525, 397);
    glVertex2f(525,384);
    glEnd();
    // Black Line
    glLineWidth(1.0);
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glVertex2f(503, 384);
    glVertex2f(503,397);
    glVertex2f(525, 397);
    glVertex2f(525,384);
    glEnd();

//Upper_Squar-part
//Within 3 part
    glColor3f(0.733, 0.871, 0.984);
    glBegin(GL_POLYGON); //1
    glVertex2f(504.5, 384);
    glVertex2f(504.5, 391);
    glVertex2f(506.6,395);
    glVertex2f(509,391);
    glVertex2f(509,384);
    glEnd();

    // Black Line
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);//1
    glVertex2f(504.5, 384);
    glVertex2f(504.5, 391);
    glVertex2f(506.6,395);
    glVertex2f(509,391);
    glVertex2f(509,384);
    glEnd();

    glColor3f(0.733, 0.871, 0.984);
    glBegin(GL_POLYGON); //2
    glVertex2f(511, 384);
    glVertex2f(511, 393);
    glVertex2f(514,396);
    glVertex2f(517,393);
    glVertex2f(517,384);
    glEnd();

    // Black Line
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glVertex2f(511, 384);
    glVertex2f(511, 393);
    glVertex2f(514,396);
    glVertex2f(517,393);
    glVertex2f(517,384);
    glEnd();

    glColor3f(0.733, 0.871, 0.984);
    glBegin(GL_POLYGON); //3
    glVertex2f(519, 384);
    glVertex2f(519, 391);
    glVertex2f(522,395);
    glVertex2f(524,391);
    glVertex2f(524,384);
    glEnd();

    // Black Line
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);//3
    glVertex2f(519, 384);
    glVertex2f(519, 391);
    glVertex2f(522,395);
    glVertex2f(524,391);
    glVertex2f(524,384);
    glEnd();


///............................
///       Right Back Minar
///............................

    glColor3f(0.945, 0.972, 0.914);
    glBegin(GL_POLYGON);
    glVertex2f(452, 198); //Below Part
    glVertex2f(483,198);
    glVertex2f(481, 235);
    glVertex2f(454,235);
    glEnd();
    // Black Line
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glVertex2f(452, 198); //Below Part
    glVertex2f(483,198);
    glVertex2f(481, 235);
    glVertex2f(454,235);
    glEnd();

    glColor3f(0.945, 0.972, 0.914);
    glBegin(GL_POLYGON);
    glVertex2f(454, 235); //Bleow thick 1st part
    glVertex2f(450, 237);
    glVertex2f(450,242);
    glVertex2f(485,242);
    glVertex2f(485,237);
    glVertex2f(481,235);
    glEnd();

    // Black Line
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glVertex2f(454, 235); //Bleow thick 1st part
    glVertex2f(450, 237);
    glVertex2f(450,242);
    glVertex2f(485,242);
    glVertex2f(485,237);
    glVertex2f(481,235);
    glEnd();

    glColor3f(0.0, 0.0, 0.0); //Single Line
    glBegin(GL_LINES);
    glVertex2f(450,237);
    glVertex2f(485, 237);
    glEnd();

//Middle Part
    glColor3f(0.945, 0.972, 0.914);
    glBegin(GL_POLYGON);
    glVertex2f(454, 242); //Middle Part
    glVertex2f(457,282);
    glVertex2f(477, 282);
    glVertex2f(480,242);
    glEnd();
    // Black Line
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glVertex2f(454, 242); //Middle Part
    glVertex2f(457,282);
    glVertex2f(477, 282);
    glVertex2f(480,242);
    glEnd();

    //Middle thik part
    glColor3f(0.945, 0.972, 0.914);
    glBegin(GL_POLYGON); // Middle thik Part
    glVertex2f(457, 282);
    glVertex2f(453, 285);
    glVertex2f(453,289);
    glVertex2f(482,289);
    glVertex2f(482,285);
    glVertex2f(477,282);
    glEnd();

    // Black Line
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glVertex2f(457, 282);
    glVertex2f(453, 285);
    glVertex2f(453,289);
    glVertex2f(482,289);
    glVertex2f(482,285);
    glVertex2f(477,282);
    glEnd();

    glColor3f(0.0, 0.0, 0.0); //Single Line
    glBegin(GL_LINES);
    glVertex2f(453,285);
    glVertex2f(482, 285);
    glEnd();

//Right Back-Minar_Upper Part
    glColor3f(0.945, 0.972, 0.914);
    glBegin(GL_POLYGON);
    glVertex2f(457, 289);
    glVertex2f(459,329);
    glVertex2f(475, 329);
    glVertex2f(477,289);
    glEnd();
    // Black Line
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glVertex2f(457, 289);
    glVertex2f(459,329);
    glVertex2f(475, 329);
    glVertex2f(477,289);
    glEnd();

//Left Back-Minar_Upper
// thik part
    glColor3f(0.945, 0.972, 0.914);
    glBegin(GL_POLYGON);
    glVertex2f(459,329);
    glVertex2f(454, 333);
    glVertex2f(458,336);
    glVertex2f(476,336);
    glVertex2f(480,333);
    glVertex2f(475, 329);
    glEnd();

    // Black Line
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glVertex2f(459,329);
    glVertex2f(454, 333);
    glVertex2f(458,336);
    glVertex2f(476,336);
    glVertex2f(480,333);
    glVertex2f(475, 329);
    glEnd();

//Right Back minar Dome
    glLineWidth(1.5);
    glColor3f(0.0, 0.0, 0.0); //Single Line
    glBegin(GL_LINES);
    glVertex2f(466.7, 354);
    glVertex2f(466.7, 361);
    glEnd();

    // Circle Outline
    glLineWidth(2.0);
    glColor3f(0.0, 0.0, 0.0); // Black color
    glBegin(GL_LINE_LOOP);
    for (int i = 0; i < 360; i++)
    {
        float angle = i * 3.14159 / 180;
        float x = 466.7 + 8 * cos(angle);
        float y = 346 + 8 * sin(angle);
        glVertex2f(x, y);
    }
    glEnd();

    // Circle Fill
    glColor3f(0.945, 0.972, 0.914);
    glBegin(GL_POLYGON);
    for (int i = 0; i < 360; i++)
    {
        float angle = i * 3.14159 / 180;
        float x = 466.7 + 8 * cos(angle);
        float y = 346 + 8 * sin(angle);
        glVertex2f(x, y);
    }
    glEnd();

//  Right_Back-Minar
//  Squar-part
    glColor3f(0.945, 0.972, 0.914);
    glBegin(GL_POLYGON);
    glVertex2f(458,336);
    glVertex2f(458,346);
    glVertex2f(476, 346);
    glVertex2f(476,336);
    glEnd();
    // Black Line
    glLineWidth(1.0);
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glVertex2f(458,336);
    glVertex2f(458,346);
    glVertex2f(476, 346);
    glVertex2f(476,336);
    glEnd();

//Upper_Squar-part
//Within 3 part
    glColor3f(0.733, 0.871, 0.984);
    glBegin(GL_POLYGON); //1
    glVertex2f(460, 336);
    glVertex2f(460, 344);
    glVertex2f(463,344);
    glVertex2f(463,336);

    glEnd();

    // Black Line
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);//1
    glVertex2f(460, 336);
    glVertex2f(460, 344);
    glVertex2f(463,344);
    glVertex2f(463,336);
    glEnd();

    glColor3f(0.733, 0.871, 0.984);
    glBegin(GL_POLYGON); //2
    glVertex2f(465, 336);
    glVertex2f(465, 344);
    glVertex2f(470,344);
    glVertex2f(470,336);

    glEnd();

    // Black Line
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);//2
    glVertex2f(465, 336);
    glVertex2f(465, 344);
    glVertex2f(470,344);
    glVertex2f(470,336);
    glEnd();

    glColor3f(0.733, 0.871, 0.984);
    glBegin(GL_POLYGON); //3
    glVertex2f(472, 336);
    glVertex2f(472, 344);
    glVertex2f(474.4,344);
    glVertex2f(474.4,336);

    glEnd();

    // Black Line
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);//3
    glVertex2f(472, 336);
    glVertex2f(472, 344);
    glVertex2f(474.4,344);
    glVertex2f(474.4,336);
    glEnd();



///.................................
///     Taj Mahal Font part
///..................................

//Main Dom Part

//Upper Triangle

    glBegin(GL_TRIANGLES);
    glColor3f(0.945, 0.972, 0.914);

    glVertex2f(270, 430); // Vertex 1
    glVertex2f(332, 430); // Vertex 2
    glVertex2f(301, 455); // Vertex 3
    glEnd();

    glLineWidth(1.0);
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glVertex2f(270, 430); // Vertex 1
    glVertex2f(332, 430); // Vertex 2
    glVertex2f(301, 455); // Vertex 3
    glEnd();

//Main Dome Upper small circle
//Smmall Circle-01
    drawCircle(301.0, 457, 5, 100);
//Smmall Circle-02
    drawCircle(301.0, 467, 4, 100);
//Smmall Circle-03
    drawCircle(301.0, 475, 3, 100);

    glColor3f(0.0, 0.0, 0.0); // Black color
    glBegin(GL_LINES);
    glVertex2f(301, 478);
    glVertex2f(301.0, 489);
    glEnd();


///..................................
///Main Dome Circle
    drawCircle(301.0, 380.0, 59.0, 100);


///......................................
/// Main Font Part
    //back-01
    glColor3f(0.945, 0.972, 0.914);
    glBegin(GL_POLYGON);
    glVertex2f(249, 198);
    glVertex2f(249,331);
    glVertex2f(353, 331);
    glVertex2f(353,198);
    glEnd();
    // Black Line
    glLineWidth(1.0);
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glVertex2f(249, 198);
    glVertex2f(249,331);
    glVertex2f(353, 331);
    glVertex2f(353,198);
    glEnd();

    //back-02
    glColor3f(0.565, 0.933, 0.565); //Deep green
    glBegin(GL_POLYGON);
    glVertex2f(260, 198);
    glVertex2f(260,318);
    glVertex2f(343, 318);
    glVertex2f(343,198);
    glEnd();
    // Black Line
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glVertex2f(260, 198);
    glVertex2f(260,318);
    glVertex2f(343, 318);
    glVertex2f(343,198);
    glEnd();

    glColor3f(0.945, 0.972, 0.914); //green
    glBegin(GL_POLYGON);//03
    glVertex2f(270, 198);
    glVertex2f(270,304);
    glVertex2f(332, 304);
    glVertex2f(332,198);
    glEnd();
    // Black Line
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);//03
    glVertex2f(270, 198);
    glVertex2f(270,304);
    glVertex2f(332, 304);
    glVertex2f(332,198);
    glEnd();


    glColor3f(0.565, 0.933, 0.565);
    glBegin(GL_POLYGON); //04
    glVertex2f(285, 198);
    glVertex2f(285,248);
    glVertex2f(317, 248);
    glVertex2f(317,198);
    glEnd();

    // Black Line
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);//04
    glVertex2f(285, 198);
    glVertex2f(285,248);
    glVertex2f(317, 248);
    glVertex2f(317,198);
    glEnd();

    glColor3f(0.945, 0.972, 0.914);
    glBegin(GL_POLYGON); //05
    glVertex2f(290, 198);
    glVertex2f(290,237);
    glVertex2f(312, 237);
    glVertex2f(312,198);
    glEnd();

    // Black Line
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);//05
    glVertex2f(290, 198);
    glVertex2f(290,237);
    glVertex2f(312, 237);
    glVertex2f(312,198);
    glEnd();

//upper line in 05
    glLineWidth(1.0);

    /* glColor3f(0.0, 0.0, 0.0); //Single Line
        glBegin(GL_LINES);
        glVertex2f(290, 224);
        glVertex2f(301, 237);

        glVertex2f(301, 237);
        glVertex2f(312, 224);
        glEnd(); */

///Main Door
glColor3f(0.2,0.2,0.2); // Deep blue color
glBegin(GL_POLYGON);
glVertex2f(295, 198);
glVertex2f(295, 217);
glVertex2f(307, 217);
glVertex2f(307, 198);
glEnd();

glColor3f(0.0f, 0.0f, 0.0f); // Black color
glBegin(GL_LINE_LOOP);
glVertex2f(295, 198);
glVertex2f(295, 217);
glVertex2f(307, 217);
glVertex2f(307, 198);
glEnd();




    // Half-Circle Outline
    glLineWidth(1.3);
    glColor3f(0.0, 0.0, 0.0); // Black color
    glBegin(GL_LINE_STRIP);
    for (int i = 0; i <= 180; i++)
    {
        float angle = i * 3.14159 / 180;
        float x = 300.7 + 30.2 * cos(angle);
        float y = 268.8 + 30.2 * sin(angle);
        glVertex2f(x, y);
    }
    glEnd();

//circle down pentagon

    glColor3f(0.725, 0.933, 0.725); //light green
    glBegin(GL_POLYGON);
    glVertex2f(290, 256);
    glVertex2f(290,272);
    glVertex2f(302, 282);
    glVertex2f(314,272);
    glVertex2f(314,256);
    glEnd();
    // Black Line
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glVertex2f(290, 256);
    glVertex2f(290,272);
    glVertex2f(302, 282);
    glVertex2f(314,272);
    glVertex2f(314,256);
    glEnd();


///.....................................
///       Taj Mahal Main BiG Dome
//.....................................


//............
    glColor3f(0.945, 0.972, 0.914);
    glBegin(GL_POLYGON);
    glVertex2f(249, 331);
    glVertex2f(249,351);
    glVertex2f(353, 351);
    glVertex2f(353,331);
    glEnd();
    // Black Line
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glVertex2f(249, 331);
    glVertex2f(249,351);
    glVertex2f(353, 351);
    glVertex2f(353,331);
    glEnd();

    glLineWidth(1.0); //LIne
    glColor3f(0.945, 0.972, 0.914);
    glBegin(GL_LINES);
    glVertex2f(249,351);
    glVertex2f(353, 351);
    glEnd();

///Dome Curve
///Curve Line -01
    glColor3f(0.0, 0.0, 0.0); // Black color
    glBegin(GL_LINE_STRIP);

    float x1 = 250.0;
    float y1 = 352.0;
    float x2 = 353.0;
    float y2 = 352.0;

    float controlPointX = (x1 + x2) / 2.0;
    float controlPointY = (y1 + y2) / 2.0 + 30.0; // Adjust the control point's Y-coordinate as needed to control the curvature

    for (float t = 0.0; t <= 1.0; t += 0.01)
    {
        float x = (1 - t) * (1 - t) * x1 + 2 * (1 - t) * t * controlPointX + t * t * x2;
        float y = (1 - t) * (1 - t) * y1 + 2 * (1 - t) * t * controlPointY + t * t * y2;

        glVertex2f(x, y);
    }

    glEnd();

///Curve Line -02

    glColor3f(0.0, 0.0, 0.0); // Black color
    glBegin(GL_LINE_STRIP);

    float x3 = 244.0;
    float y3 = 362.0;
    float x4 = 358.0;
    float y4 = 362.0;

    float controlPointXx = (x3 + x4) / 2.0;
    float controlPointYy = (y3 + y4) / 2.0 + 30.0; // Adjust the control point's Y-coordinate as needed to control the curvature

    for (float t = 0.0; t <= 1.0; t += 0.01)
    {
        float x = (1 - t) * (1 - t) * x3 + 2 * (1 - t) * t * controlPointXx  + t * t * x4;
        float y = (1 - t) * (1 - t) * y3 + 2 * (1 - t) * t * controlPointYy + t * t * y4;

        glVertex2f(x, y);
    }

    glEnd();

// Black Line between the curve line
    // Small Lines
    /* glColor3f(0.0, 0.0, 0.0); // Black color
    glBegin(GL_LINES);
    glVertex2f(353.0, 352.0);
    glVertex2f(328.0, 357.0);

    glEnd(); */



///.................................
///     Taj Mahal 1st Left part
///..................................

    //back-01
    glColor3f(0.945, 0.972, 0.914);
    glBegin(GL_POLYGON);
    glVertex2f(194, 198);
    glVertex2f(194,310);
    glVertex2f(250, 310);
    glVertex2f(250,198);
    glEnd();
    // Black Line
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glVertex2f(194, 198);
    glVertex2f(194,310);
    glVertex2f(250, 310);
    glVertex2f(250,198);
    glEnd();

    //top singl line
    glColor3f(0.0, 0.0, 0.0); //Single Line
    glBegin(GL_LINES);
    glVertex2f(194,303);
    glVertex2f(250, 303);
    glEnd();

    //Up box left 1st

    //box-01
    glColor3f(0.725, 0.933, 0.725); //light green
    glBegin(GL_POLYGON);
    glVertex2f(210, 250);
    glVertex2f(210,295);
    glVertex2f(240, 295);
    glVertex2f(240,250);
    glEnd();
    // Black Line
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glVertex2f(210, 250);
    glVertex2f(210,295);
    glVertex2f(240, 295);
    glVertex2f(240,250);
    glEnd();

    glLineWidth(2.0); //LIne
    glColor3f(0.0, 0.0, 0.0); //Single Line
    glBegin(GL_LINES);

    glVertex2f(210, 277);
    glVertex2f(225, 292);

    glVertex2f(225, 292);
    glVertex2f(240, 277);
    glEnd();

//balck windo door up
    glColor3f(0.2, 0.2, 0.2); // Light black color
    glBegin(GL_POLYGON);
    glVertex2f(220, 252);
    glVertex2f(220,268);
    glVertex2f(230, 268);
    glVertex2f(230,252);
    glEnd();

//Lower box left 2nd below
    //box-01
    glColor3f(0.725, 0.933, 0.725); //light green
    glBegin(GL_POLYGON);
    glVertex2f(210, 198);
    glVertex2f(210,244);
    glVertex2f(240, 244);
    glVertex2f(240,198);
    glEnd();
    // Black Line
    glLineWidth(1.0); //LIne
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glVertex2f(210, 198);
    glVertex2f(210,244);
    glVertex2f(240, 244);
    glVertex2f(240,198);
    glEnd();

    glLineWidth(2.0); //LIne
    glColor3f(0.0, 0.0, 0.0); //Single Line
    glBegin(GL_LINES);

    glVertex2f(210, 224);
    glVertex2f(225, 239);

    glVertex2f(225, 239);
    glVertex2f(240, 224);
    glEnd();

//balck windo door below
    glColor3f(0.2, 0.2, 0.2); // Light black color
    glBegin(GL_POLYGON);
    glVertex2f(220, 198);
    glVertex2f(220,215);
    glVertex2f(230, 215);
    glVertex2f(230,198);
    glEnd();

// Left thik Minar
    glColor3f(0.945, 0.972, 0.914);
    glBegin(GL_POLYGON);
    glVertex2f(190, 198);
    glVertex2f(194,198);
    glVertex2f(194, 333);
    glVertex2f(190,333);
    glEnd();
    // Black Line
    glLineWidth(1.0); //LIne
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glVertex2f(190, 198);
    glVertex2f(194,198);
    glVertex2f(194, 333);
    glVertex2f(190,333);
    glEnd();

    //Main Minar of thik
    glColor3f(0.945, 0.972, 0.914);
    glBegin(GL_POLYGON);
    glVertex2f(190, 333);
    glVertex2f(188,335.5);
    glVertex2f(192, 339);
    glVertex2f(196,335.5);
    glVertex2f(194, 333);
    glEnd();
    // Black Line
    glLineWidth(1.0); //LIne
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glVertex2f(190, 333);
    glVertex2f(188,335.5);
    glVertex2f(192, 339);
    glVertex2f(196,335.5);
    glVertex2f(194, 333);
    glEnd();

    //upper line
    glColor3f(0.0, 0.0, 0.0); //Single Line
    glBegin(GL_LINES);
    glVertex2f(192, 339);
    glVertex2f(192, 345);
    glEnd();




    ///.................................//
    ///    Dome circle left 1st block
    ///.................................//

    // Circle Outline
    glLineWidth(2.0); // Set the line width to 2.0 (you can adjust this value as needed)
    glColor3f(0.0, 0.0, 0.0); // Black color
    glBegin(GL_LINE_LOOP);
    for (int i = 0; i <= 360; i++)
    {
        float angle = i * 3.14159 / 180;
        float x = 228 + 21 * cos(angle);
        float y = 338 + 21 * sin(angle);
        glVertex2f(x, y);
    }
    glEnd();

    // Circle Fill
    glColor3f(0.945, 0.972, 0.914); // Light color
    glBegin(GL_TRIANGLE_FAN);
    glVertex2f(228, 338); // Center point
    for (int i = 0; i <= 360; i++)
    {
        float angle = i * 3.14159 / 180;
        float x = 228 + 21 * cos(angle);
        float y = 338 + 21 * sin(angle);
        glVertex2f(x, y);
    }
    glEnd();

//Top Minar part left 1st block
    glColor3f(0.945, 0.972, 0.914);
    glBegin(GL_POLYGON);
    glVertex2f(206, 310);
    glVertex2f(206,338);
    glVertex2f(250,338);
    glVertex2f(250, 310);
    glEnd();
    // Black Line
    glLineWidth(1.0); //LIne
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glVertex2f(206, 310);
    glVertex2f(206,338);
    glVertex2f(250,338);
    glVertex2f(250, 310);
    glEnd();
    // line
    glColor3f(0.0, 0.0, 0.0); //Single Line
    glBegin(GL_LINES);
    glVertex2f(206,331);
    glVertex2f(250,331);
    glEnd();

// Black Darak Spacek //
// 3 part
    glColor3f(0.2, 0.2, 0.2);
    glBegin(GL_POLYGON); //1
    glVertex2f(210, 310);
    glVertex2f(210, 320);
    glVertex2f(214,325);
    glVertex2f(218,320);
    glVertex2f(218,310);
    glEnd();

    glColor3f(0.2, 0.2, 0.2);
    glBegin(GL_POLYGON); //2
    glVertex2f(222, 310);
    glVertex2f(222, 320);
    glVertex2f(227.5,328);
    glVertex2f(234,320);
    glVertex2f(234,310);
    glEnd();

    glColor3f(0.2, 0.2, 0.2);
    glBegin(GL_POLYGON); //3
    glVertex2f(238, 310);
    glVertex2f(238, 320);
    glVertex2f(242.5,325);
    glVertex2f(247,320);
    glVertex2f(247,310);
    glEnd();



    //uppler long line
    glLineWidth(2.0); //LIne
    glColor3f(0.0, 0.0, 0.0); //Single Line
    glBegin(GL_LINES);
    glVertex2f(228, 359);
    glVertex2f(228,372);
    glEnd();


///.................................
///     Taj Mahal 2nd Left part
///..................................
    //box-01
    glColor3f(0.945, 0.972, 0.914);
    glBegin(GL_POLYGON);
    glVertex2f(167, 198);
    glVertex2f(167,306);
    glVertex2f(190, 310);
    glVertex2f(190,198);
    glEnd();
    // Black Line
    glLineWidth(1.0); //LIne
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glVertex2f(167, 198);
    glVertex2f(167,306);
    glVertex2f(190, 310);
    glVertex2f(190,198);
    glEnd();

    glColor3f(0.0, 0.0, 0.0); //Single Line
    glBegin(GL_LINES);

    glVertex2f(167, 299);
    glVertex2f(190,303);
    glEnd();

//up box-01
    glColor3f(0.725, 0.933, 0.725); //light green
    glBegin(GL_POLYGON);
    glVertex2f(171, 248);
    glVertex2f(171,290);
    glVertex2f(186, 290);
    glVertex2f(186,248);
    glEnd();
    // Black Line
    glLineWidth(1.0); //LIne
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glBegin(GL_POLYGON);
    glVertex2f(171, 248);
    glVertex2f(171,290);
    glVertex2f(186, 290);
    glVertex2f(186,248);
    glEnd();

    glLineWidth(1.4); //LIne
    glColor3f(0.0, 0.0, 0.0); //Single Line
    glBegin(GL_LINES);

    glVertex2f(171, 278);
    glVertex2f(178, 289);

    glVertex2f(178, 289);
    glVertex2f(186, 278);
    glEnd();


//up box-02
    glColor3f(0.725, 0.933, 0.725); //light green
    glBegin(GL_POLYGON);
    glVertex2f(171, 198);
    glVertex2f(171,240);
    glVertex2f(186, 240);
    glVertex2f(186,198);
    glEnd();
    // Black Line
    glLineWidth(1.0); //LIne
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glBegin(GL_POLYGON);
    glVertex2f(171, 198);
    glVertex2f(171,240);
    glVertex2f(186, 240);
    glVertex2f(186,198);
    glEnd();

    glLineWidth(1.4); //LIne
    glColor3f(0.0, 0.0, 0.0); //Single Line
    glBegin(GL_LINES);

    glVertex2f(171, 228);
    glVertex2f(178, 238);

    glVertex2f(178, 238);
    glVertex2f(186, 228);
    glEnd();
///.................................
///          left 2nd thik Minar
/// 2nd Left thik Minar

    glColor3f(0.945, 0.972, 0.914);
    glBegin(GL_POLYGON);
    glVertex2f(162, 198);
    glVertex2f(167,198);
    glVertex2f(167, 328);
    glVertex2f(162,328);
    glEnd();
    // Black Line
    glLineWidth(1.0); //LIne
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glVertex2f(162, 198);
    glVertex2f(167,198);
    glVertex2f(167, 328);
    glVertex2f(162,328);
    glEnd();

    //Main Minar of thik
    glColor3f(0.945, 0.972, 0.914);
    glBegin(GL_POLYGON);
    glVertex2f(162,328);
    glVertex2f(160,331);
    glVertex2f(164, 335);
    glVertex2f(169,332);
    glVertex2f(167, 328);
    glEnd();
    // Black Line
    glLineWidth(1.0); //LIne
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glVertex2f(162,328);
    glVertex2f(160,331);
    glVertex2f(164, 335);
    glVertex2f(169,331);
    glVertex2f(167, 328);
    glEnd();

    //upper line
    glColor3f(0.0, 0.0, 0.0); //Single Line
    glBegin(GL_LINES);
    glVertex2f(164, 335);
    glVertex2f(164, 340);
    glEnd();

/// 2nd Left Upper Extra part

    glColor3f(0.945, 0.972, 0.914);
    glBegin(GL_POLYGON);
    glVertex2f(167, 306);
    glVertex2f(167,324);
    glVertex2f(176, 324);
    glVertex2f(176,308);
    glEnd();
    // Black Line
    glLineWidth(1.0); //LIne
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glBegin(GL_POLYGON);
    glVertex2f(167, 306);
    glVertex2f(167,324);
    glVertex2f(176, 324);
    glVertex2f(176,308);
    glEnd();

    glColor3f(0.945, 0.972, 0.914);
    glBegin(GL_POLYGON);
    glVertex2f(176,308);
    glVertex2f(176, 324);
    glVertex2f(186, 316);
    glVertex2f(186,309);
    glEnd();
    // Black Line
    glLineWidth(1.0); //LIne
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glBegin(GL_POLYGON);
    glVertex2f(176,308);
    glVertex2f(176, 324);
    glVertex2f(186, 316);
    glVertex2f(186,309);
    glEnd();



///.................................
///     Taj Mahal 1st Right part
///..................................
//back-01
    glColor3f(0.945, 0.972, 0.914);
    glBegin(GL_POLYGON);
    glVertex2f(353, 198);
    glVertex2f(353,310);
    glVertex2f(407, 310);
    glVertex2f(407,198);
    glEnd();
    // Black Line
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glVertex2f(353, 198);
    glVertex2f(353,310);
    glVertex2f(407, 310);
    glVertex2f(407,198);
    glEnd();

    //top singl line
    glColor3f(0.0, 0.0, 0.0); //Single Line
    glBegin(GL_LINES);
    glVertex2f(353,303);
    glVertex2f(407, 303);
    glEnd();

//Up box left 1st
    //box-01
    glColor3f(0.725, 0.933, 0.725); //light green
    glBegin(GL_POLYGON);
    glVertex2f(360, 250);
    glVertex2f(360,295);
    glVertex2f(395, 295);
    glVertex2f(395,250);
    glEnd();
    // Black Line
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glVertex2f(360, 250);
    glVertex2f(360,295);
    glVertex2f(395, 295);
    glVertex2f(395,250);
    glEnd();

    glLineWidth(2.0); //LIne
    glColor3f(0.0, 0.0, 0.0); //Single Line
    glBegin(GL_LINES);

    glVertex2f(360, 277);
    glVertex2f(377, 292);

    glVertex2f(377, 292);
    glVertex2f(395, 277);
    glEnd();

    //......................
    //balck windo door up
    glColor3f(0.2, 0.2, 0.2); // Light black color
    glBegin(GL_POLYGON);
    glVertex2f(372, 252);
    glVertex2f(372,268);
    glVertex2f(382, 268);
    glVertex2f(382,252);
    glEnd();

//Lower box left 2nd below
    //box-01
    glColor3f(0.725, 0.933, 0.725); //light green
    glBegin(GL_POLYGON);
    glVertex2f(360, 198);
    glVertex2f(360,244);
    glVertex2f(395, 244);
    glVertex2f(395,198);
    glEnd();
    // Black Line
    glLineWidth(1.0); //LIne
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glVertex2f(360, 198);
    glVertex2f(360,244);
    glVertex2f(395, 244);
    glVertex2f(395,198);
    glEnd();

    glLineWidth(2.0); //LIne
    glColor3f(0.0, 0.0, 0.0); //Single Line
    glBegin(GL_LINES);

    glVertex2f(360, 224);
    glVertex2f(377, 239);

    glVertex2f(377, 239);
    glVertex2f(395, 224);
    glEnd();

//balck windo door below
    glColor3f(0.2, 0.2, 0.2); // Light black color
    glBegin(GL_POLYGON);
    glVertex2f(372, 198);
    glVertex2f(372,215);
    glVertex2f(382, 215);
    glVertex2f(382,198);
    glEnd();
//......................................
// Left thik Minar
    glColor3f(0.945, 0.972, 0.914);
    glBegin(GL_POLYGON);
    glVertex2f(407, 198);
    glVertex2f(412,198);
    glVertex2f(412, 333);
    glVertex2f(407,333);
    glEnd();
    // Black Line
    glLineWidth(1.0); //LIne
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glVertex2f(407, 198);
    glVertex2f(412,198);
    glVertex2f(412, 333);
    glVertex2f(407,333);
    glEnd();

    //Main Minar of thik
    glColor3f(0.945, 0.972, 0.914);
    glBegin(GL_POLYGON);
    glVertex2f(407, 333);
    glVertex2f(405,335.5);
    glVertex2f(409, 339);
    glVertex2f(414,335.5);
    glVertex2f(412, 333);
    glEnd();
    // Black Line
    glLineWidth(1.0); //LIne
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glVertex2f(407, 333);
    glVertex2f(405,335.5);
    glVertex2f(409, 339);
    glVertex2f(414,335.5);
    glVertex2f(412, 333);
    glEnd();

    //upper line
    glColor3f(0.0, 0.0, 0.0); //Single Line
    glBegin(GL_LINES);
    glVertex2f(409, 339);
    glVertex2f(409, 345);
    glEnd();

///.................................//
///    Dome circle Right 1st block
///.................................//

    // Circle Outline
    glLineWidth(2.0); // Set the line width to 2.0 (you can adjust this value as needed)
    glColor3f(0.0, 0.0, 0.0); // Black color
    glBegin(GL_LINE_LOOP);
    for (int i = 0; i <= 360; i++)
    {
        float angle = i * 3.14159 / 180;
        float x = 374.5 + 21 * cos(angle);
        float y = 338 + 21 * sin(angle);
        glVertex2f(x, y);
    }
    glEnd();

    // Circle Fill
    glColor3f(0.945, 0.972, 0.914); // Light color
    glBegin(GL_TRIANGLE_FAN);
    glVertex2f(374.5, 338); // Center point
    for (int i = 0; i <= 360; i++)
    {
        float angle = i * 3.14159 / 180;
        float x = 374.5 + 21 * cos(angle);
        float y = 338 + 21 * sin(angle);
        glVertex2f(x, y);
    }
    glEnd();

//..............................

///Top Minar part Right 1st block
    glColor3f(0.945, 0.972, 0.914);
    glBegin(GL_POLYGON);
    glVertex2f(353, 310);
    glVertex2f(353,338);
    glVertex2f(396,338);
    glVertex2f(396, 310);
    glEnd();
    // Black Line
    glLineWidth(1.0); //LIne
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glVertex2f(353, 310);
    glVertex2f(353,338);
    glVertex2f(396,338);
    glVertex2f(396, 310);
    glEnd();
    // line
    glColor3f(0.0, 0.0, 0.0); //Single Line
    glBegin(GL_LINES);
    glVertex2f(353,331);
    glVertex2f(396,331);
    glEnd();

// Black Darak Spacek //
// 3 part
    glColor3f(0.2, 0.2, 0.2);
    glBegin(GL_POLYGON); //1
    glVertex2f(356, 310);
    glVertex2f(356, 320);
    glVertex2f(360,325);
    glVertex2f(364,320);
    glVertex2f(364,310);
    glEnd();

    glColor3f(0.2, 0.2, 0.2);
    glBegin(GL_POLYGON); //2
    glVertex2f(368, 310);
    glVertex2f(368, 320);
    glVertex2f(374.5,328);
    glVertex2f(380,320);
    glVertex2f(380,310);
    glEnd();

    glColor3f(0.2, 0.2, 0.2);
    glBegin(GL_POLYGON); //3
    glVertex2f(385, 310);
    glVertex2f(385, 320);
    glVertex2f(389,325);
    glVertex2f(393,320);
    glVertex2f(393,310);
    glEnd();

    //uppler long line
    glLineWidth(2.0); //LIne
    glColor3f(0.0, 0.0, 0.0); //Single Line
    glBegin(GL_LINES);
    glVertex2f(374.5, 359);
    glVertex2f(374.5,372);
    glEnd();

///.................................
///     Taj Mahal 2nd Right part
///..................................
    //box-01
    glColor3f(0.945, 0.972, 0.914);
    glBegin(GL_POLYGON);
    glVertex2f(412, 198);
    glVertex2f(412,310);
    glVertex2f(435, 306);
    glVertex2f(435,198);
    glEnd();
    // Black Line
    glLineWidth(1.0); //LIne
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glVertex2f(412, 198);
    glVertex2f(412,310);
    glVertex2f(435, 306);
    glVertex2f(435,198);
    glEnd();

    glColor3f(0.0, 0.0, 0.0); //Single Line
    glBegin(GL_LINES);

    glVertex2f(435, 299);
    glVertex2f(412,303);
    glEnd();

//..............
//up box-01
    glColor3f(0.725, 0.933, 0.725); //light green
    glBegin(GL_POLYGON);
    glVertex2f(416, 248);
    glVertex2f(416,290);
    glVertex2f(431, 290);
    glVertex2f(431,248);
    glEnd();
    // Black Line
    glLineWidth(1.0); //LIne
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glBegin(GL_POLYGON);
    glVertex2f(416, 248);
    glVertex2f(416,290);
    glVertex2f(431, 290);
    glVertex2f(431,248);
    glEnd();

    glLineWidth(1.4); //LIne
    glColor3f(0.0, 0.0, 0.0); //Single Line
    glBegin(GL_LINES);

    glVertex2f(416, 278);
    glVertex2f(423.5, 289);

    glVertex2f(423.5, 289);
    glVertex2f(431, 278);
    glEnd();

//up box-02
    glColor3f(0.725, 0.933, 0.725); //light green
    glBegin(GL_POLYGON);
    glVertex2f(416, 198);
    glVertex2f(416,240);
    glVertex2f(431, 240);
    glVertex2f(431,198);
    glEnd();
    // Black Line
    glLineWidth(1.0); //LIne
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glBegin(GL_POLYGON);
    glVertex2f(416, 198);
    glVertex2f(416,240);
    glVertex2f(431, 240);
    glVertex2f(431,198);
    glEnd();

    glLineWidth(1.4); //LIne
    glColor3f(0.0, 0.0, 0.0); //Single Line
    glBegin(GL_LINES);

    glVertex2f(416, 228);
    glVertex2f(423.5, 238);

    glVertex2f(423.5, 238);
    glVertex2f(431, 228);
    glEnd();

///.................................
///        left 2nd thik Minar
///.................................

// 2nd Left thik Minar
    glColor3f(0.945, 0.972, 0.914);
    glBegin(GL_POLYGON);
    glVertex2f(435, 198);
    glVertex2f(440,198);
    glVertex2f(440, 328);
    glVertex2f(435,328);
    glEnd();
    // Black Line
    glLineWidth(1.0); //LIne
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glVertex2f(435, 198);
    glVertex2f(440,198);
    glVertex2f(440, 328);
    glVertex2f(435,328);
    glEnd();

    //Main Minar of thik
    glColor3f(0.945, 0.972, 0.914);
    glBegin(GL_POLYGON);
    glVertex2f(435,328);
    glVertex2f(432,331);
    glVertex2f(437.5, 335);
    glVertex2f(443,332);
    glVertex2f(440, 328);
    glEnd();
    // Black Line
    glLineWidth(1.0); //LIne
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glVertex2f(435,328);
    glVertex2f(432,331);
    glVertex2f(437.5, 335);
    glVertex2f(443,332);
    glVertex2f(440, 328);
    glEnd();

    //upper line
    glColor3f(0.0, 0.0, 0.0); //Single Line
    glBegin(GL_LINES);
    glVertex2f(437.5, 335);
    glVertex2f(437.5, 340);
    glEnd();
//..............................
// 2nd Left Upper Extra part

    glColor3f(0.945, 0.972, 0.914);
    glBegin(GL_POLYGON);
    glVertex2f(425, 308);
    glVertex2f(425,324);
    glVertex2f(435, 324);
    glVertex2f(435,306);
    glEnd();
    // Black Line
    glLineWidth(1.0); //LIne
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glBegin(GL_POLYGON);
    glBegin(GL_POLYGON);
    glVertex2f(425, 308);
    glVertex2f(425,324);
    glVertex2f(435, 324);
    glVertex2f(435,306);
    glEnd();

    glColor3f(0.945, 0.972, 0.914);
    glBegin(GL_POLYGON);
    glVertex2f(415,309);
    glVertex2f(415, 316);
    glVertex2f(425, 324);
    glVertex2f(425,308);
    glEnd();
    // Black Line
    glLineWidth(1.0); //LIne
    glColor3f(0.0, 0.0, 0.0);
    glBegin(GL_LINE_LOOP);
    glBegin(GL_POLYGON);
    glBegin(GL_POLYGON);
    glVertex2f(415,309);
    glVertex2f(415, 316);
    glVertex2f(425, 324);
    glVertex2f(425,308);
    glEnd();

///===============================
///          Rain              ///
///===============================

if (isRainStarted)
    {
        rainOn();

    }

    glFlush();
    glutSwapBuffers();

}
void handleKeypress(unsigned char key, int x, int y)
{
    switch (key)
    {
        case 'r':
        case 'R':
            isRainActive = true;
            isRainStarted = true;
            PlaySound(TEXT("rain-07.wav"), NULL, SND_ASYNC);
            break;
        case 's':
        case 'S':
            PlaySound(NULL, 0, 0); // Stop the rain sound
            isRainActive = false;
            isRainStarted = false;
            break;
    }
}


void init (void)
{
    glClearColor (0.0, 0.0, 0.0, 0.0);
    glMatrixMode(GL_PROJECTION);
    glLoadIdentity();
    glOrtho(0.0, 600, 0.0, 600, -10.0, 10.0);
}

int main(int argc, char** argv)
{
    glutInit(&argc, argv);
    glutInitDisplayMode (GLUT_SINGLE | GLUT_RGB);
    glutInitWindowSize (900, 900);
    glutInitWindowPosition (200,50);
    glutCreateWindow ("Taj Mahal");

    PlaySound(TEXT("bird-2.wav"), NULL, SND_ASYNC);

///rain
    for (size_t i = 0; i < 1000; ++i)
    {
        Point pt;
        pt.x = rand() % 600;  // Use window width instead of fixed value
        pt.y = rand() % 600;
        pt.r = 255;
        pt.g = 255;
        pt.b = 255;
        pt.a = 255;
        points.push_back(pt);
    }

    glutTimerFunc(100, rain, 0);
    init ();
    glutDisplayFunc(display);
    glutTimerFunc(0, update, 0);

    glutKeyboardFunc(handleKeypress);
    glutMainLoop();

    return 0;
}
