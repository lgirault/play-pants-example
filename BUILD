# Reverse routes
routes_library(
        name='reverse_routes',
        sources=['conf/routes'],
        generate_forward_router = False,
        generate_reverse_router = True,
        dependencies=['3rdparty/jvm:play']
        )

twirl_library(
        name='views',
        sources=rglobs('app/views/*.html'),
        source_dir='app',
        dependencies=[
            '3rdparty/jvm:play', 
            '3rdparty/jvm:twirl-api',
            ':reverse_routes'
        ])

scala_library(name='demo_app_lib',
              sources=rglobs('app/*.scala'),
              dependencies=['3rdparty/jvm:play', ':views'])

# Forward routes need the app.
routes_library(
        name='forward_routes',
        sources=['conf/routes'],
        generate_forward_router = True,
        generate_reverse_router = False,
        dependencies=[':demo_app_lib']
        )

resources(name='public_assets', sources=rglobs('public/*'))

jvm_binary(name='demo-bin',
           resources=['conf:play-conf', ':public_assets'],
           main='play.core.server.ProdServerStart',
           dependencies=[
               ':demo_app_lib', 
               ':forward_routes', 
               '3rdparty/jvm:play-server', 
               '3rdparty/jvm:play-logback',
               '3rdparty/jvm:play-netty-server'
           ])

