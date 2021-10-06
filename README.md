#include <iostream>
#include <cmath>
#include <boost/math/quadrature/gauss_kronrod.hpp>
#include <boost/random.hpp>
boost::random::mt19937 rng(time(NULL));
using namespace std;
using namespace boost::math::quadrature;
struct point2
{
    double x;
    double y;
};

struct point3
{
    double x;
    double y;
    double z;
};
double f(double x, double y);
double grad(double (*f)(double,double),double ax, double bx, double ay, double by);
double MK(double (*f)(double, double), double ax, double bx, double ay, double by, double az, double bz );

int main()
{
    cout<<MK(f,0,1,0,1,0,2)<<endl;
    return 0;
}

double f(double x, double y)
{
    return x*x+y*y;
}

double grad(double (*f)(double,double),double ax, double bx, double ay, double by)
{
    double dx, dy;
    double res, check;
    res =0;
    check = res;
    dx = 1e-4;
    dy = dx;
    point2 M;
    M.x = (bx - ax)/2;
    M.y = (by - by)/2;
    return 0;
}

double MK(double (*f)(double, double), double ax, double bx, double ay, double by, double az, double bz )
{
    double V;
    double x, y,z;
    int n,N;
    V = (bx - ax)*(by - ay)*(bz- az);
    N = 1e8;
    n = 0;
   boost::random::uniform_real_distribution<double>genx(ax,bx);
   boost::random::uniform_real_distribution<double>geny(ay,by);
   boost::random::uniform_real_distribution<double>genz(az,bz);
    for(int i=0; i<N; i++)
    {
        x = genx(rng);
        y = geny(rng);
        z = genz(rng);
        if(z < f(x,y))
        {
            n++;
        }

    }

    return V*n/N;
}


